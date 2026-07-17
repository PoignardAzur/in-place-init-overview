# Asahi Monster Struct

## Premise

The Asahi Linux project defines [a giant `HwDataA` struct in `initdata.rs`](https://github.com/AsahiLinux/linux/blob/1986be38e7f6b294adcc851698a66db5a4427055/drivers/gpu/drm/asahi/fw/initdata.rs#L226-L589):

```rust
#[versions(AGX)]
#[repr(C)]
pub(crate) struct HwDataA {
  pub(crate) unk_0: u32,
  pub(crate) clocks_per_period: u32,

  #[ver(V >= V13_0B4)]
  pub(crate) clocks_per_period_2: u32,

  pub(crate) unk_8: u32,
  pub(crate) pwr_status: AtomicU32,
  pub(crate) unk_10: F32,
  pub(crate) unk_14: u32,
  pub(crate) unk_18: u32,
  pub(crate) unk_1c: u32,
  pub(crate) unk_20: u32,
  pub(crate) unk_24: u32,
  pub(crate) actual_pstate: u32,
  pub(crate) tgt_pstate: u32,
  pub(crate) unk_30: u32,
  pub(crate) cur_pstate: u32,
  pub(crate) unk_38: u32,

  // ... 266 more fields ...

  #[ver(V >= V13_0B4)]
  pub(crate) aux_leak_coef: AuxLeakCoef,
  #[ver(V >= V13_0B4)]
  pub(crate) unk_3d34_0: Array<0x18, u8>,

  pub(crate) unk_3d34: Array<0x38, u8>,
}
```

That struct is initialized [in `hwdata_a()](https://github.com/AsahiLinux/linux/blob/1986be38e7f6b294adcc851698a66db5a4427055/drivers/gpu/drm/asahi/initdata.rs#L245-L488):


```rust
fn hwdata_a(&mut self) -> Result<GpuObject<HwDataA::ver>> {
  let pwr = &self.dyncfg.pwr;
  let period_ms = pwr.power_sample_period;
  let period_s = F32::from(period_ms) / f32!(1000.0);
  // ... 18 more decls ...

  self.alloc
    .private
    .new_init(pin_init::init_zeroed(), |_inner, _ptr| {
      let cfg = &self.cfg;
      let dyncfg = &self.dyncfg;
      try_init!(raw::HwDataA::ver {
        clocks_per_period: clocks_per_period,
        #[ver(V >= V13_0B4)]
        clocks_per_period_2: clocks_per_period,
        pwr_status: AtomicU32::new(4),
        unk_10: f32!(1.0),
        actual_pstate: 1,
        tgt_pstate: 1,
        base_pstate_scaled: base_ps_scaled,
        unk_40: 1,
        max_pstate_scaled: max_ps_scaled,
        min_pstate_scaled: 100,
        unk_64c: 625,
        pwr_filter_a_neg: f32!(1.0) - pwr_filter_a,
        pwr_filter_a: pwr_filter_a,
        pwr_integral_gain: pwr.pwr_integral_gain,
        pwr_integral_min_clamp: pwr.pwr_integral_min_clamp.into(),
        // ... ~100 more fields ...
        max_pstate_scaled_14: max_ps_scaled,
        t81xx_data <- Self::t81xx_data(cfg, dyncfg),
        #[ver(V >= V13_0B4)]
        unk_e10_0 <- {
          let filter_a = f32!(1.0) / pwr.se_filter_time_constant.into();
          let filter_1_a = f32!(1.0) / pwr.se_filter_time_constant_1.into();
          try_init!(raw::HwDataA130Extra {
            unk_38: 4,
            unk_3c: 8000,
            // ... 35 more fields ...
            max_pstate_scaled_2: max_ps_scaled,
            ..Zeroable::init_zeroed()
          })
        },
        fast_die0_sensor_mask_2: U64(cfg.fast_sensor_mask[0]),
        #[ver(G >= G14X)]
        fast_die1_sensor_mask_2: U64(cfg.fast_sensor_mask[1]),
        unk_e24: cfg.da.unk_e24,
        unk_e28: 1,
        fast_die0_sensor_mask_alt: U64(cfg.fast_sensor_mask_alt[0]),
        #[ver(G >= G14X)]
        fast_die1_sensor_mask_alt: U64(cfg.fast_sensor_mask_alt[1]),
        #[ver(V < V13_0B4)]
        fast_die0_sensor_present: U64(cfg.fast_die0_sensor_present as u64),
        unk_163c: 1,
        unk_3644: 0,
        hws1 <- Self::hw_shared1(cfg),
        hws2 <- Self::hw_shared2(cfg, dyncfg),
        hws3 <- Self::hw_shared3(cfg),
        unk_3ce8: 1,
        ..Zeroable::init_zeroed()
      })
      .chain(|raw| {
        for i in 0..self.dyncfg.pwr.perf_states.len() {
          raw.sram_k[i] = self.cfg.sram_k;
        }

        for (i, coef) in pwr.core_leak_coef.iter().enumerate() {
          raw.core_leak_coef[i] = *coef;
        }

        for (i, coef) in pwr.sram_leak_coef.iter().enumerate() {
          raw.sram_leak_coef[i] = *coef;
        }

        #[ver(V >= V13_0B4)]
        if let Some(csafr) = pwr.csafr.as_ref() {
          for (i, coef) in csafr.leak_coef_afr.iter().enumerate() {
            raw.aux_leak_coef.cs_1[i] = *coef;
            raw.aux_leak_coef.cs_2[i] = *coef;
          }

          for (i, coef) in csafr.leak_coef_cs.iter().enumerate() {
            raw.aux_leak_coef.afr_1[i] = *coef;
            raw.aux_leak_coef.afr_2[i] = *coef;
          }
        }

        // ... 3 for-loops ...

        Ok(())
      })
    })
}
```

## Problem statement

**Rewrite `hwdata_a` using your proposed syntax.**

For the sake of brevity, you make skip fields in the same places the snippet above did:

- After `let period_s`.
- Between `pwr_integral_min_clamp` and `max_pstate_scaled_14`.
- Between `unk_3c` and `max_pstate_scaled_2`.
- The last three `for` loops.

Whenever your example changes syntax compared to the snippet above, insert a `// MODIFIED` above the changed line/paragraph.


## Solution template

```rust
// PROPOSAL

fn hwdata_a(&mut self) -> Result<GpuObject<HwDataA::ver>> {
  // ...
}
```
