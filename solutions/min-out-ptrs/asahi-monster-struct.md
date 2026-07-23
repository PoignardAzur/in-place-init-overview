# Asahi Monster Struct

```rust
// PROPOSAL

fn hwdata_a(&mut self) -> Result<GpuObject<HwDataA::ver>> {
  let pwr = &self.dyncfg.pwr;
  let period_ms = pwr.power_sample_period;
  let period_s = F32::from(period_ms) / f32!(1000.0);
  // ... 18 more decls ...

  self.alloc
    .private
    // MODIFIED
    .new_init(pin_init::init_zeroed(), |raw, _inner, _ptr| {
      let cfg = &self.cfg;
      let dyncfg = &self.dyncfg;

      // MODIFIED
      let raw = raw <- raw::HwDataA::ver {
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
        // MODIFIED
        t81xx_data <- Self::t81xx_data(&uninit raw.t81xx_data, cfg, dyncfg)?,
        #[ver(V >= V13_0B4)]
        unk_e10_0 <- {
          let filter_a = f32!(1.0) / pwr.se_filter_time_constant.into();
          let filter_1_a = f32!(1.0) / pwr.se_filter_time_constant_1.into();

          // MODIFIED
          let extra = &uninit raw.unk_e10_0;
          extra <- raw::HwDataA130Extra {
            unk_38: 4,
            unk_3c: 8000,
            // ... 35 more fields ...
            max_pstate_scaled_2: max_ps_scaled,
            ..Zeroable::init_zeroed()
          }
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
        // MODIFIED
        hws1 <- Self::hw_shared1(&uninit raw.hws1, cfg)?,
        hws2 <- Self::hw_shared2(&uninit raw.hws2, cfg, dyncfg)?,
        hws3 <- Self::hw_shared3(&uninit raw.hws3, cfg)?,
        unk_3ce8: 1,
        ..Zeroable::init_zeroed()
      })

      // MODIFIED - Removed .chain(...) wrapper

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

      // MODIFIED
      Ok(raw)
    })
})
}
```
