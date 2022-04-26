<template>
<div class="q-pa-md bg-dark text-white">
    <div class="row">
        <div class="col-lg-3 col-xs-12 q-pa-sm">
            <div class="q-pa-sm bg-grey-10" style="height:100%" bordered>
                <div class="text-h6 q-pa-md q-pt-lg">PID Status</div>
                <q-separator />
                <div class="row q-pt-md">
                    <div class="col-12">
                        <div class="q-gutter-y-md q-pa-sm">
                            <!-- <q-select dark v-model="mode" :options="options" label="Mode"  /> -->
                            <q-input dark filled v-model="PID001.VAL"  input-class="text-right" dense debouce='2000' type='number'>
                                        <template v-slot:before>
                                            <div class="text-caption medium">
                                                Setpoint
                                            </div>
                                        </template>
                                        <template v-slot:after>
                                            <q-avatar>
                                            </q-avatar>
                                        </template>
                                    </q-input>
                              <div class="q-pt-md">
                                <q-slider
                                  v-model="PID001.VAL"
                                  label
                                  label-always
                                  :label-value="`Setpoint:  ${PID001.VAL}`"
                                  :min="0.0"
                                  :max="400.0"
                                  :step="0.1"
                                  debounce="1000"
                                >
                                  <template v-slot:before>
                                    <div class="text-caption medium">
                                        Process Variable
                                    </div>
                                </template>
                                </q-slider>
                              </div>
                            <!-- <q-input dark filled v-model="actuator" label="Actuator" ></q-input> -->
                            <q-input dark filled v-model="PID001.CVAL" input-class="text-right" dense >
                                 <template v-slot:before>
                                    <div class="text-caption medium">
                                        Process Variable
                                    </div>
                                </template>
                                 <template v-slot:after>
                                    <q-avatar>
                                    </q-avatar>
                                </template>
                            </q-input>
                            <q-input dark filled v-model="processGain" input-class="text-right" dense debouce='2000'>
                                 <template v-slot:before>
                                    <div class="text-caption medium">
                                        Process Gain
                                    </div>
                                </template>
                                 <template v-slot:after>
                                    <q-avatar>
                                    </q-avatar>
                                </template>
                            </q-input>
                            <div class="q-pt-md">
                                <q-slider
                                  v-model="processGain"
                                  label
                                  label-always
                                  :label-value="`Process Gain:  ${processGain}`"
                                  :min="1.5"
                                  :max="3.0"
                                  :step="0.01"
                                  debounce="1000"
                                >
                                  <template v-slot:before>
                                    <div class="text-caption medium">
                                        Process Variable
                                    </div>
                                </template>
                                </q-slider>
                              </div>
                            <q-input dark filled v-model="PID001.OVAL" input-class="text-right" dense readonly>
                                 <template v-slot:before>
                                    <div class="text-caption medium">
                                        Output
                                    </div>
                                </template>
                                 <template v-slot:after>
                                    <q-avatar>
                                        %
                                    </q-avatar>
                                </template>
                            </q-input>
                            <!-- <q-input dark filled v-model="readback" input-class="text-right" dense readonly>
                                <template v-slot:before>
                                    <div class="text-caption medium">
                                        Readback
                                    </div>
                                </template>
                                <template v-slot:after>
                                    <q-avatar>
                                        %
                                    </q-avatar>
                                </template>
                            </q-input> -->
                        </div>
                    </div>
                </div>
                <div class="text-h6 q-pa-md q-pt-xl">PID Parameters</div>
                <q-separator />
                <div class="row q-pt-md">
                  <div class="col-12">
                  </div>
                    <div class="col-6">
                        <div class="text text-left q-pl-md q-pb-sm" style="font-size:16px">Settings</div>
                        <q-separator class="q-mb-sm" />
                        <div class="q-gutter-y-md q-pa-sm">
                            <q-input dark filled v-model="PID001.MAX" input-class="text-center" debounce="1000" dense>
                                <template v-slot:before>
                                    <div class="text-caption small">
                                        Max Output
                                    </div>
                                </template>
                                <template v-slot:after>
                                    <q-avatar>
                                        %
                                    </q-avatar>
                                </template>
                            </q-input>
                            <q-input dark filled v-model="PID001.MIN" input-class="text-center" debounce="1000" dense>
                                <template v-slot:before>
                                    <div class="text-caption small">
                                        Min Output
                                    </div>
                                </template>
                                <template v-slot:after>
                                    <q-avatar>
                                        %
                                    </q-avatar>
                                </template>
                            </q-input>
                            <q-input dark filled v-model="rampRate" input-class="text-center" debounce="1000" dense>
                                <template v-slot:before>
                                    <div class="text-caption small">
                                        Ramp Rate
                                    </div>
                                </template>
                                <template v-slot:after>
                                    <q-avatar>
                                        %/s
                                    </q-avatar>
                                </template>
                            </q-input>
                            <q-input dark filled v-model="minChange" input-class="text-center" debounce="1000" dense>
                                <template v-slot:before>
                                    <div class="text-caption small">
                                        Min Change
                                    </div>
                                </template>
                                <template v-slot:after>
                                    <q-avatar>
                                        %
                                    </q-avatar>
                                </template>
                            </q-input>
                            <q-input dark filled v-model="PID001.MDt" input-class="text-center" debounce="1000" dense>
                                <template v-slot:before>
                                    <div class="text-caption small">
                                        Sample Time
                                    </div>
                                </template>
                                <template v-slot:after>
                                    <q-avatar>
                                        s
                                    </q-avatar>
                                </template>
                            </q-input>
                        </div>
                    </div>
                    <div class="col-6">
                      <div class="text text-left q-pl-md q-pb-sm q-ml-lg" style="font-size:16px">Tuning</div>
                        <q-separator class="q-mb-sm q-ml-lg" />
                        <div class="q-gutter-y-md q-pa-sm">
                            <q-input dark filled v-model="PID001.KP" input-class="text-center" debounce="1000" dense>
                                <template v-slot:before>
                                    <div class="text-caption small text-center">
                                        Kp
                                    </div>
                                </template>
                            </q-input>
                            <q-input dark filled v-model="PID001.KI" input-class="text-center" debounce="1000" dense>
                                <template v-slot:before>
                                    <div class="text-caption small text-center">
                                        Ki
                                    </div>
                                </template>
                            </q-input>
                            <q-input dark filled v-model="PID001.KD" input-class="text-center" debounce="1000" dense>
                                <template v-slot:before>
                                    <div class="text-caption small text-center">
                                        Kd
                                    </div>
                                </template>
                            </q-input>
                            <!-- <q-toggle
                            class="q-px-xl"
                              input-class="text-left"
                              v-model="toggle"
                              label="On Right"
                            /> -->
                        </div>
                    </div>
                </div>
                <div class="text-h6 q-pa-md q-pt-xl">PID Calculation</div>
                <q-separator />
                <div class="row q-pt-md">
                  <div class="col-12">
                  </div>
                  <div class="q-pa-md bg-grey-10 text-white">
                    <q-list dark separator style="max-width: 100%">
                      <q-item clickable v-ripple>
                       <q-item-section avatar>
                          <q-avatar color="primary" text-color="white" size="md">
                            P
                          </q-avatar>
                        </q-item-section>
                        <q-item-section>{{ PID001.p }}</q-item-section>
                      </q-item>
                    </q-list>
                    <q-item clickable v-ripple>
                       <q-item-section avatar>
                          <q-avatar color="secondary" text-color="white" size="md">
                            I
                          </q-avatar>
                        </q-item-section>
                        <q-item-section>{{ PID001.iSUM }}</q-item-section>
                      </q-item>
                    <q-item clickable v-ripple>
                       <q-item-section avatar>
                          <q-avatar color="accent" text-color="white" size="md">
                            D
                          </q-avatar>
                        </q-item-section>
                        <q-item-section>{{ PID001.d }}</q-item-section>
                      </q-item>
                      <q-item clickable v-ripple>
                       <q-item-section avatar>
                            Sample Count:
                        </q-item-section>
                        <q-item-section>{{ this.seriesData[0].data.length }}</q-item-section>
                      </q-item>
                  </div>
                </div>
            </div>
        </div>
        <div class="col-lg-9 col-xs-12 q-pa-sm">
            <div class="row q-pa-sm bg-dark" bordered>
                <div class="text-h6 q-pa-md">Performance Chart</div>
                <div class="col-12">
                    <chart-container :seriesData="seriesData" :PID001="PID001" />
                </div>
            </div>
        </div>
    </div>
    <div class="row" style="height: 900px; max-height: 50%">
        <div class="col-12 q-pa-sm">
            <div class="q-pa-sm bg-grey-10" style="height:100%"></div>
        </div>
    </div>
</div>
</template>

<script>
import ChartContainer from 'src/containers/ChartContainer.vue'
import {
  defineComponent,
  ref
} from 'vue'

export default defineComponent({
  name: 'ParamterContainer',
  components: {
    ChartContainer
  },
  props: {
    title: {
      type: String,
      required: true
    }
  },
  setup () {
    return {
      mode: ref(''),
      options: [
        'Auto', 'Manual', 'Off'
      ],
      actuator: false,
      readback: ref('0.0'),
      maxOutput: ref('100.0'),
      minOutput: ref('0.0'),
      rampRate: ref('1.0'),
      minChange: ref('0.01'),
      sampleTime: ref('1.0')
    }
  },
  data () {
    return {
      seriesData: [
        {
          name: 'PV',
          data: []
        },
        {
          name: 'SP',
          data: []
        },
        {
          name: 'CO',
          data: []
        }
      ],
      toggle: false,
      maxSamples: 10000,
      processGain: 2.16,
      PID001: {
        CVAL: 200.0,
        OVAL: 92.5,
        MIN: 0.0,
        MAX: 100.0,
        DMIN: 0.0,
        DMAX: 100.0,
        VAL: 200.0,
        KP: 0.075,
        KI: 0.001,
        KD: 0.0,
        err: 0,
        derr: 0,
        MDt: 1.0,
        dt: 1.001,
        dm: 0.00,
        odm: 0.0,
        ct: Date.now(),
        AVAL: 0.0,
        p: 0.0,
        i: 0.0,
        d: 0.0,
        iSUM: 0.0
      }
    }
  },
  created () {
    this.timedCount()
  },
  methods: {
    show_details (p, i, d, e) {
      // console.log( PID001);
      console.log(`p = ${p}, i = ${i}, d = ${d}`)
      console.log(this.seriesData)
    },
    calculate_pid (dt, ct) {
      const dtp = this.PID001.dt //  difference in time previous
      const dep = this.PID001.derr
      const e = this.PID001.VAL - this.PID001.CVAL

      const de = e - this.PID001.err
      console.log('error is', e, 'de is ', de)
      const p = this.PID001.KP * de
      const i = this.PID001.KI * e * dt
      let d = 0.0
      if (dt > 0 && dtp > 0) d = this.PID001.KD * (de / dt - (dep / dtp))
      if (dt <= 0 || dtp <= 0) d = 0

      const dm = p + i + d
      this.update_record(dt, ct, e, de, dm, p, i, d)
      //  console.log(dm);
      this.show_details(p, i, d, e)
    },
    update_record (dt, ct, e, de, dm, p, i, d) {
      const last = this.PID001.OVAL
      this.PID001.dt = dt
      this.PID001.err = e
      this.PID001.derr = de
      this.PID001.ct = ct
      if ((dm + last) < this.PID001.MIN) dm = this.PID001.MIN - last
      if ((dm + last) > this.PID001.MAX) dm = this.PID001.MAX - last

      let mdm = Math.abs(dm)

      if (mdm > this.PID001.DMAX) mdm = this.PID001.DMAX
      if (mdm < this.PID001.DMIN) mdm = 0

      if (dm > 0) dm = mdm
      if (dm < 0) dm = 0 - mdm

      this.PID001.p = p
      this.PID001.i = i
      this.PID001.d = d
      this.PID001.iSUM = this.PID001.iSUM + i
      this.PID001.AVAL = this.PID001.OVAL + dm
      this.PID001.dm = dm
      this.PID001.odm = this.PID001.dm

      this.PID001.OVAL = this.PID001.AVAL
      console.log(this.seriesData.length)
      //   if (this.seriesData[0].data.length < 10) {
      //     this.seriesData[0].data.push(
      //       [this.PID001.ct, this.PID001.CVAL]
      //     )
      //   }
      this.seriesData[0].data.push([this.PID001.ct, this.PID001.CVAL])
      this.seriesData[1].data.push([this.PID001.ct, this.PID001.VAL])
      this.seriesData[2].data.push([this.PID001.ct, this.PID001.OVAL])
    },
    timedCount () {
      const ctp = this.PID001.ct
      const ct = Date.now()
      const dt = (ct - ctp) / 1000

      this.PID001.dm = 0
      // console.log(dt);
      if (dt > this.PID001.MDt && this.seriesData[0].data.length < this.maxSamples) {
        this.calculate_pid(dt, ct)
        let sign = 1
        if (this.PID001.KP < 0.0) {
          sign = -1.0
        } else {
          sign = 1.0
        }
        this.PID001.CVAL = (this.PID001.OVAL * sign) * this.processGain
        //  this.PID001.CVAL = this.PID001.CVAL + this.PID001.OVAL * sign * this.processGain
        //  this.PID001.CVAL = Math.random() * (25 - 0) + 0
      }

      setTimeout(this.timedCount, 500)
    }
  }
})
</script>
<style lang="scss" scoped>
.small {
  width: 80px;
}
.medium {
  width: 120px;
}
</style>
