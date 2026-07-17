```rust
/// <https://github.com/AsahiLinux/linux/blob/asahi/drivers/gpu/drm/asahi/fw/initdata.rs#L222-L583>
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


    #[ver(V >= V13_0B4)]
    pub(crate) unk_3c_0: u32,


    pub(crate) base_pstate_scaled: u32,
    pub(crate) unk_40: u32,
    pub(crate) max_pstate_scaled: u32,
    pub(crate) unk_48: u32,
    pub(crate) min_pstate_scaled: u32,
    pub(crate) freq_mhz: F32,
    pub(crate) unk_54: Array<0x20, u8>,


    #[ver(V >= V13_0B4)]
    pub(crate) unk_74_0: u32,


    pub(crate) sram_k: Array<0x10, F32>,
    pub(crate) unk_b4: Array<0x100, u8>,
    pub(crate) unk_1b4: u32,
    pub(crate) temp_c: u32,
    pub(crate) avg_power_mw: u32,
    pub(crate) update_ts: U64,
    pub(crate) unk_1c8: u32,
    pub(crate) unk_1cc: Array<0x478, u8>,
    pub(crate) pad_644: Pad<0x8>,
    pub(crate) unk_64c: u32,
    pub(crate) unk_650: u32,
    pub(crate) pad_654: u32,
    pub(crate) pwr_filter_a_neg: F32,
    pub(crate) pad_65c: u32,
    pub(crate) pwr_filter_a: F32,
    pub(crate) pad_664: u32,
    pub(crate) pwr_integral_gain: F32,
    pub(crate) pad_66c: u32,
    pub(crate) pwr_integral_min_clamp: F32,
    pub(crate) max_power_1: F32,
    pub(crate) pwr_proportional_gain: F32,
    pub(crate) pad_67c: u32,
    pub(crate) pwr_pstate_related_k: F32,
    pub(crate) pwr_pstate_max_dc_offset: i32,
    pub(crate) unk_688: u32,
    pub(crate) max_pstate_scaled_2: u32,
    pub(crate) pad_690: u32,
    pub(crate) unk_694: u32,
    pub(crate) max_power_2: u32,
    pub(crate) pad_69c: Pad<0x18>,
    pub(crate) unk_6b4: u32,


    #[ver(V >= V13_0B4)]
    pub(crate) unk_6b8_0: Array<0x10, u8>,


    pub(crate) max_pstate_scaled_3: u32,
    pub(crate) unk_6bc: u32,
    pub(crate) pad_6c0: Pad<0x14>,
    pub(crate) ppm_filter_tc_periods_x4: u32,
    pub(crate) unk_6d8: u32,
    pub(crate) pad_6dc: u32,
    pub(crate) ppm_filter_a_neg: F32,
    pub(crate) pad_6e4: u32,
    pub(crate) ppm_filter_a: F32,
    pub(crate) pad_6ec: u32,
    pub(crate) ppm_ki_dt: F32,
    pub(crate) pad_6f4: u32,
    pub(crate) pwr_integral_min_clamp_2: u32,
    pub(crate) unk_6fc: F32,
    pub(crate) ppm_kp: F32,
    pub(crate) pad_704: u32,
    pub(crate) unk_708: u32,
    pub(crate) pwr_min_duty_cycle: u32,
    pub(crate) max_pstate_scaled_4: u32,
    pub(crate) unk_714: u32,
    pub(crate) pad_718: u32,
    pub(crate) unk_71c: F32,
    pub(crate) max_power_3: u32,
    pub(crate) cur_power_mw_2: u32,
    pub(crate) ppm_filter_tc_ms: u32,
    pub(crate) unk_72c: u32,


    #[ver(V >= V13_0B4)]
    pub(crate) ppm_filter_tc_clks: u32,


    #[ver(V >= V13_0B4)]
    pub(crate) unk_730_4: u32,


    #[ver(V >= V13_0B4)]
    pub(crate) unk_730_8: u32,


    #[ver(V >= V13_0B4)]
    pub(crate) unk_730_c: u32,


    pub(crate) unk_730: F32,
    pub(crate) unk_734: u32,
    pub(crate) unk_738: u32,
    pub(crate) unk_73c: u32,
    pub(crate) unk_740: u32,
    pub(crate) unk_744: u32,
    pub(crate) unk_748: Array<0x4, F32>,
    pub(crate) unk_758: u32,
    pub(crate) perf_tgt_utilization: u32,
    pub(crate) pad_760: u32,
    pub(crate) perf_boost_min_util: u32,
    pub(crate) perf_boost_ce_step: u32,
    pub(crate) perf_reset_iters: u32,
    pub(crate) pad_770: u32,
    pub(crate) unk_774: u32,
    pub(crate) unk_778: u32,
    pub(crate) perf_filter_drop_threshold: u32,
    pub(crate) perf_filter_a_neg: F32,
    pub(crate) perf_filter_a2_neg: F32,
    pub(crate) perf_filter_a: F32,
    pub(crate) perf_filter_a2: F32,
    pub(crate) perf_ki: F32,
    pub(crate) perf_ki2: F32,
    pub(crate) perf_integral_min_clamp: F32,
    pub(crate) unk_79c: F32,
    pub(crate) perf_kp: F32,
    pub(crate) perf_kp2: F32,
    pub(crate) boost_state_unk_k: F32,
    pub(crate) base_pstate_scaled_2: u32,
    pub(crate) max_pstate_scaled_5: u32,
    pub(crate) base_pstate_scaled_3: u32,
    pub(crate) pad_7b8: u32,
    pub(crate) perf_cur_utilization: F32,
    pub(crate) perf_tgt_utilization_2: u32,
    pub(crate) pad_7c4: Pad<0x18>,
    pub(crate) unk_7dc: u32,


    #[ver(V >= V13_0B4)]
    pub(crate) unk_7e0_0: Array<0x10, u8>,


    pub(crate) base_pstate_scaled_4: u32,
    pub(crate) pad_7e4: u32,
    pub(crate) unk_7e8: Array<0x14, u8>,
    pub(crate) unk_7fc: F32,
    pub(crate) pwr_min_duty_cycle_2: F32,
    pub(crate) max_pstate_scaled_6: F32,
    pub(crate) max_freq_mhz: u32,
    pub(crate) pad_80c: u32,
    pub(crate) unk_810: u32,
    pub(crate) pad_814: u32,
    pub(crate) pwr_min_duty_cycle_3: u32,
    pub(crate) unk_81c: u32,
    pub(crate) pad_820: u32,
    pub(crate) min_pstate_scaled_4: F32,
    pub(crate) max_pstate_scaled_7: u32,
    pub(crate) unk_82c: u32,
    pub(crate) unk_alpha_neg: F32,
    pub(crate) unk_alpha: F32,
    pub(crate) unk_838: u32,
    pub(crate) unk_83c: u32,
    pub(crate) pad_840: Pad<0x2c>,
    pub(crate) unk_86c: u32,
    pub(crate) fast_die0_sensor_mask: U64,
    #[ver(G >= G14X)]
    pub(crate) fast_die1_sensor_mask: U64,
    pub(crate) fast_die0_release_temp_cc: u32,
    pub(crate) unk_87c: i32,
    pub(crate) unk_880: u32,
    pub(crate) unk_884: u32,
    pub(crate) pad_888: u32,
    pub(crate) unk_88c: u32,
    pub(crate) pad_890: u32,
    pub(crate) unk_894: F32,
    pub(crate) pad_898: u32,
    pub(crate) fast_die0_ki_dt: F32,
    pub(crate) pad_8a0: u32,
    pub(crate) unk_8a4: u32,
    pub(crate) unk_8a8: F32,
    pub(crate) fast_die0_kp: F32,
    pub(crate) pad_8b0: u32,
    pub(crate) unk_8b4: u32,
    pub(crate) pwr_min_duty_cycle_4: u32,
    pub(crate) max_pstate_scaled_8: u32,
    pub(crate) max_pstate_scaled_9: u32,
    pub(crate) fast_die0_prop_tgt_delta: u32,
    pub(crate) unk_8c8: u32,
    pub(crate) unk_8cc: u32,
    pub(crate) pad_8d0: Pad<0x14>,


    #[ver(V >= V13_0B4)]
    pub(crate) unk_8e4_0: Array<0x10, u8>,


    pub(crate) unk_8e4: u32,
    pub(crate) unk_8e8: u32,
    pub(crate) max_pstate_scaled_10: u32,
    pub(crate) unk_8f0: u32,
    pub(crate) unk_8f4: u32,
    pub(crate) pad_8f8: u32,
    pub(crate) pad_8fc: u32,
    pub(crate) unk_900: Array<0x24, u8>,


    pub(crate) unk_coef_a1: Array<8, Array<MAX_CORES_PER_CLUSTER::ver, F32>>,
    pub(crate) unk_coef_a2: Array<8, Array<MAX_CORES_PER_CLUSTER::ver, F32>>,


    pub(crate) pad_b24: Pad<0x70>,
    pub(crate) max_pstate_scaled_11: u32,
    pub(crate) freq_with_off: u32,
    pub(crate) unk_b9c: u32,
    pub(crate) unk_ba0: U64,
    pub(crate) unk_ba8: U64,
    pub(crate) unk_bb0: u32,
    pub(crate) unk_bb4: u32,


    #[ver(V >= V13_3)]
    pub(crate) pad_bb8_0: Pad<0x200>,
    #[ver(V >= V13_5)]
    pub(crate) pad_bb8_200: Pad<0x8>,


    pub(crate) pad_bb8: Pad<0x74>,
    pub(crate) unk_c2c: u32,
    pub(crate) power_zone_count: u32,
    pub(crate) max_power_4: u32,
    pub(crate) max_power_5: u32,
    pub(crate) max_power_6: u32,
    pub(crate) unk_c40: u32,
    pub(crate) unk_c44: F32,
    pub(crate) avg_power_target_filter_a_neg: F32,
    pub(crate) avg_power_target_filter_a: F32,
    pub(crate) avg_power_target_filter_tc_x4: u32,
    pub(crate) avg_power_target_filter_tc_xperiod: u32,


    #[ver(V >= V13_0B4)]
    pub(crate) avg_power_target_filter_tc_clks: u32,


    #[ver(V >= V13_0B4)]
    pub(crate) unk_c58_4: u32,


    pub(crate) power_zones: Array<5, PowerZone::ver>,
    pub(crate) avg_power_filter_tc_periods_x4: u32,
    pub(crate) unk_cfc: u32,
    pub(crate) unk_d00: u32,
    pub(crate) avg_power_filter_a_neg: F32,
    pub(crate) unk_d08: u32,
    pub(crate) avg_power_filter_a: F32,
    pub(crate) unk_d10: u32,
    pub(crate) avg_power_ki_dt: F32,
    pub(crate) unk_d18: u32,
    pub(crate) unk_d1c: u32,
    pub(crate) unk_d20: F32,
    pub(crate) avg_power_kp: F32,
    pub(crate) unk_d28: u32,
    pub(crate) unk_d2c: u32,
    pub(crate) avg_power_min_duty_cycle: u32,
    pub(crate) max_pstate_scaled_12: u32,
    pub(crate) max_pstate_scaled_13: u32,
    pub(crate) unk_d3c: u32,
    pub(crate) max_power_7: F32,
    pub(crate) max_power_8: u32,
    pub(crate) unk_d48: u32,
    pub(crate) avg_power_filter_tc_ms: u32,
    pub(crate) unk_d50: u32,


    #[ver(V >= V13_0B4)]
    pub(crate) avg_power_filter_tc_clks: u32,


    #[ver(V >= V13_0B4)]
    pub(crate) unk_d54_4: Array<0xc, u8>,


    pub(crate) unk_d54: Array<0x10, u8>,
    pub(crate) max_pstate_scaled_14: u32,
    pub(crate) unk_d68: Array<0x24, u8>,


    pub(crate) t81xx_data: T81xxData,


    pub(crate) unk_dd0: Array<0x40, u8>,


    #[ver(V >= V13_2)]
    pub(crate) unk_e10_pad: Array<0x10, u8>,


    #[ver(V >= V13_0B4)]
    pub(crate) unk_e10_0: HwDataA130Extra,


    pub(crate) unk_e10: Array<0xc, u8>,


    pub(crate) fast_die0_sensor_mask_2: U64,
    #[ver(G >= G14X)]
    pub(crate) fast_die1_sensor_mask_2: U64,


    pub(crate) unk_e24: u32,
    pub(crate) unk_e28: u32,
    pub(crate) unk_e2c: Pad<0x1c>,
    pub(crate) unk_coef_b1: Array<8, Array<MAX_CORES_PER_CLUSTER::ver, F32>>,
    pub(crate) unk_coef_b2: Array<8, Array<MAX_CORES_PER_CLUSTER::ver, F32>>,


    #[ver(G >= G14X)]
    pub(crate) pad_1048_0: Pad<0x600>,


    pub(crate) pad_1048: Pad<0x5e4>,


    pub(crate) fast_die0_sensor_mask_alt: U64,
    #[ver(G >= G14X)]
    pub(crate) fast_die1_sensor_mask_alt: U64,
    #[ver(V < V13_0B4)]
    pub(crate) fast_die0_sensor_present: U64,


    pub(crate) unk_163c: u32,


    pub(crate) unk_1640: Array<0x2000, u8>,


    #[ver(G >= G14X)]
    pub(crate) unk_3640_0: Array<0x2000, u8>,


    pub(crate) unk_3640: u32,
    pub(crate) unk_3644: u32,
    pub(crate) hws1: HwDataShared1,


    #[ver(V >= V13_0B4)]
    pub(crate) unk_hws2: Array<16, u16>,


    pub(crate) hws2: HwDataShared2,
    pub(crate) unk_3c00: u32,
    pub(crate) unk_3c04: u32,
    pub(crate) hws3: HwDataShared3,
    pub(crate) unk_3c58: Array<0x3c, u8>,
    pub(crate) unk_3c94: u32,
    pub(crate) unk_3c98: U64,
    pub(crate) unk_3ca0: U64,
    pub(crate) unk_3ca8: U64,
    pub(crate) unk_3cb0: U64,
    pub(crate) ts_last_idle: U64,
    pub(crate) ts_last_poweron: U64,
    pub(crate) ts_last_poweroff: U64,
    pub(crate) unk_3cd0: U64,
    pub(crate) unk_3cd8: U64,


    #[ver(V >= V13_0B4)]
    pub(crate) unk_3ce0_0: u32,


    pub(crate) unk_3ce0: u32,
    pub(crate) unk_3ce4: u32,
    pub(crate) unk_3ce8: u32,
    pub(crate) unk_3cec: u32,
    pub(crate) unk_3cf0: u32,
    pub(crate) core_leak_coef: Array<8, F32>,
    pub(crate) sram_leak_coef: Array<8, F32>,


    #[ver(V >= V13_0B4)]
    pub(crate) aux_leak_coef: AuxLeakCoef,
    #[ver(V >= V13_0B4)]
    pub(crate) unk_3d34_0: Array<0x18, u8>,


    pub(crate) unk_3d34: Array<0x38, u8>,
}
```

```rust
// <https://github.com/AsahiLinux/linux/blob/asahi/drivers/gpu/drm/asahi/initdata.rs#L236-L478>
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
    max_power_1: pwr.max_power_mw.into(),
    pwr_proportional_gain: pwr.pwr_proportional_gain,
    pwr_pstate_related_k: -F32::from(max_ps_scaled) / pwr.max_power_mw.into(),
    pwr_pstate_max_dc_offset: pwr.pwr_min_duty_cycle as i32 - max_ps_scaled as i32,
    max_pstate_scaled_2: max_ps_scaled,
    max_power_2: pwr.max_power_mw,
    max_pstate_scaled_3: max_ps_scaled,
    ppm_filter_tc_periods_x4: ppm_filter_tc_periods * 4,
    ppm_filter_a_neg: f32!(1.0) - ppm_filter_a,
    ppm_filter_a: ppm_filter_a,
    ppm_ki_dt: pwr.ppm_ki * period_s,
    unk_6fc: f32!(65536.0),
    ppm_kp: pwr.ppm_kp,
    pwr_min_duty_cycle: pwr.pwr_min_duty_cycle,
    max_pstate_scaled_4: max_ps_scaled,
    unk_71c: f32!(0.0),
    max_power_3: pwr.max_power_mw,
    cur_power_mw_2: 0x0,
    ppm_filter_tc_ms: pwr.ppm_filter_time_constant_ms,
    #[ver(V >= V13_0B4)]
    ppm_filter_tc_clks: ppm_filter_tc_ms_rounded * base_clock_khz,
    perf_tgt_utilization: pwr.perf_tgt_utilization,
    perf_boost_min_util: pwr.perf_boost_min_util,
    perf_boost_ce_step: pwr.perf_boost_ce_step,
    perf_reset_iters: pwr.perf_reset_iters,
    unk_774: 6,
    unk_778: 1,
    perf_filter_drop_threshold: pwr.perf_filter_drop_threshold,
    perf_filter_a_neg: f32!(1.0) - perf_filter_a,
    perf_filter_a2_neg: f32!(1.0) - perf_filter_a2,
    perf_filter_a: perf_filter_a,
    perf_filter_a2: perf_filter_a2,
    perf_ki: pwr.perf_integral_gain,
    perf_ki2: pwr.perf_integral_gain2,
    perf_integral_min_clamp: pwr.perf_integral_min_clamp.into(),
    unk_79c: f32!(95.0),
    perf_kp: pwr.perf_proportional_gain,
    perf_kp2: pwr.perf_proportional_gain2,
    boost_state_unk_k: F32::from(boost_ps_count) / f32!(0.95),
    base_pstate_scaled_2: base_ps_scaled,
    max_pstate_scaled_5: max_ps_scaled,
    base_pstate_scaled_3: base_ps_scaled,
    perf_tgt_utilization_2: pwr.perf_tgt_utilization,
    base_pstate_scaled_4: base_ps_scaled,
    unk_7fc: f32!(65536.0),
    pwr_min_duty_cycle_2: pwr.pwr_min_duty_cycle.into(),
    max_pstate_scaled_6: max_ps_scaled.into(),
    max_freq_mhz: pwr.max_freq_mhz,
    pwr_min_duty_cycle_3: pwr.pwr_min_duty_cycle,
    min_pstate_scaled_4: f32!(100.0),
    max_pstate_scaled_7: max_ps_scaled,
    unk_alpha_neg: f32!(0.8),
    unk_alpha: f32!(0.2),
    fast_die0_sensor_mask: U64(cfg.fast_sensor_mask[0]),
    #[ver(G >= G14X)]
    fast_die1_sensor_mask: U64(cfg.fast_sensor_mask[1]),
    fast_die0_release_temp_cc: 100 * pwr.fast_die0_release_temp,
    unk_87c: cfg.da.unk_87c,
    unk_880: 0x4,
    unk_894: f32!(1.0),

    fast_die0_ki_dt: pwr.fast_die0_integral_gain * period_s,
    unk_8a8: f32!(65536.0),
    fast_die0_kp: pwr.fast_die0_proportional_gain,
    pwr_min_duty_cycle_4: pwr.pwr_min_duty_cycle,
    max_pstate_scaled_8: max_ps_scaled,
    max_pstate_scaled_9: max_ps_scaled,
    fast_die0_prop_tgt_delta: 100 * pwr.fast_die0_prop_tgt_delta,
    unk_8cc: cfg.da.unk_8cc,
    max_pstate_scaled_10: max_ps_scaled,
    max_pstate_scaled_11: max_ps_scaled,
    unk_c2c: 1,
    power_zone_count: pwr.power_zones.len() as u32,
    max_power_4: pwr.max_power_mw,
    max_power_5: pwr.max_power_mw,
    max_power_6: pwr.max_power_mw,
    avg_power_target_filter_a_neg: f32!(1.0) - avg_power_target_filter_a,
    avg_power_target_filter_a: avg_power_target_filter_a,
    avg_power_target_filter_tc_x4: 4 * pwr.avg_power_target_filter_tc,
    avg_power_target_filter_tc_xperiod: period_ms * pwr.avg_power_target_filter_tc,
    #[ver(V >= V13_0B4)]
    avg_power_target_filter_tc_clks: period_ms
        * pwr.avg_power_target_filter_tc
        * base_clock_khz,
    avg_power_filter_tc_periods_x4: 4 * avg_power_filter_tc_periods,
    avg_power_filter_a_neg: f32!(1.0) - avg_power_filter_a,
    avg_power_filter_a: avg_power_filter_a,
    avg_power_ki_dt: pwr.avg_power_ki_only * period_s,
    unk_d20: f32!(65536.0),
    avg_power_kp: pwr.avg_power_kp,
    avg_power_min_duty_cycle: pwr.avg_power_min_duty_cycle,
    max_pstate_scaled_12: max_ps_scaled,
    max_pstate_scaled_13: max_ps_scaled,
    max_power_7: pwr.max_power_mw.into(),
    max_power_8: pwr.max_power_mw,
    avg_power_filter_tc_ms: pwr.avg_power_filter_tc_ms,
    #[ver(V >= V13_0B4)]
    avg_power_filter_tc_clks: avg_power_filter_tc_ms_rounded * base_clock_khz,
    max_pstate_scaled_14: max_ps_scaled,
    t81xx_data <- Self::t81xx_data(cfg, dyncfg),
    #[ver(V >= V13_0B4)]
    unk_e10_0 <- {
        let filter_a = f32!(1.0) / pwr.se_filter_time_constant.into();
        let filter_1_a = f32!(1.0) / pwr.se_filter_time_constant_1.into();
        try_init!(raw::HwDataA130Extra {
            unk_38: 4,
            unk_3c: 8000,
            gpu_se_inactive_threshold: pwr.se_inactive_threshold,
            gpu_se_engagement_criteria: pwr.se_engagement_criteria,
            gpu_se_reset_criteria: pwr.se_reset_criteria,
            unk_54: 50,
            unk_58: 0x1,
            gpu_se_filter_a_neg: f32!(1.0) - filter_a,
            gpu_se_filter_1_a_neg: f32!(1.0) - filter_1_a,
            gpu_se_filter_a: filter_a,
            gpu_se_filter_1_a: filter_1_a,
            gpu_se_ki_dt: pwr.se_ki * period_s,
            gpu_se_ki_1_dt: pwr.se_ki_1 * period_s,
            unk_7c: f32!(65536.0),
            gpu_se_kp: pwr.se_kp,
            gpu_se_kp_1: pwr.se_kp_1,

            #[ver(V >= V13_3)]
            unk_8c: 100,
            #[ver(V < V13_3)]
            unk_8c: 40,

            max_pstate_scaled_1: max_ps_scaled,
            unk_9c: f32!(8000.0),
            unk_a0: 1400,
            gpu_se_filter_time_constant_ms: pwr.se_filter_time_constant * period_ms,
            gpu_se_filter_time_constant_1_ms: pwr.se_filter_time_constant_1
                * period_ms,
            gpu_se_filter_time_constant_clks: U64((pwr.se_filter_time_constant
                * clocks_per_period_coarse)
                .into()),
            gpu_se_filter_time_constant_1_clks: U64((pwr
                .se_filter_time_constant_1
                * clocks_per_period_coarse)
                .into()),
            unk_c4: f32!(65536.0),
            unk_114: f32!(65536.0),
            unk_124: 40,
            max_pstate_scaled_2: max_ps_scaled,
            ..Zeroable::zeroed()
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
    ..Zeroable::zeroed()
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

    for i in 0..self.dyncfg.id.num_clusters as usize {
        if let Some(coef_a) = self.cfg.unk_coef_a.get(i) {
            (*raw.unk_coef_a1[i])[..coef_a.len()].copy_from_slice(coef_a);
            (*raw.unk_coef_a2[i])[..coef_a.len()].copy_from_slice(coef_a);
        }
        if let Some(coef_b) = self.cfg.unk_coef_b.get(i) {
            (*raw.unk_coef_b1[i])[..coef_b.len()].copy_from_slice(coef_b);
            (*raw.unk_coef_b2[i])[..coef_b.len()].copy_from_slice(coef_b);
        }
    }

    for (i, pz) in pwr.power_zones.iter().enumerate() {
        raw.power_zones[i].target = pz.target;
        raw.power_zones[i].target_off = pz.target - pz.target_offset;
        raw.power_zones[i].filter_tc_x4 = 4 * pz.filter_tc;
        raw.power_zones[i].filter_tc_xperiod = period_ms * pz.filter_tc;
        let filter_a = f32!(1.0) / pz.filter_tc.into();
        raw.power_zones[i].filter_a = filter_a;
        raw.power_zones[i].filter_a_neg = f32!(1.0) - filter_a;
        #[ver(V >= V13_0B4)]
        raw.power_zones[i].unk_10 = 1320000000;
    }

    #[ver(V >= V13_0B4 && G >= G14X)]
    for (i, j) in raw.hws2.g14.curve2.t1.iter().enumerate() {
        raw.unk_hws2[i] = if *j == 0xffff { 0 } else { j / 2 };
    }

    Ok(())
})
```
