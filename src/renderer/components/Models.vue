<template>
    <div class="ctrl-set ctrl-set-models">
        <div class="ctrl-set-header">
            <div class="ctrl-set-title">
                Models
                <small class="ctrl-set-stats">({{selectedIndex}}/{{total}} Selected)</small>
                &nbsp;
                <a href="javascript:void(0)" class="ctrl-set-clear" @click="clearModels">Clear</a>
            </div>

            <ModelSearch/>
        </div>
        <div class="ctrl-set-body">
            <b-row>
                <ModelList name="Calibrated" :models="modelsCalibrated"/>
                <ModelList name="Estimated US" :models="modelsEstimatedUs"/>
                <ModelList name="Estimated Euro Area" :models="modelsEstimatedEuroArea"/>
                <ModelList name="Estimated/Calibrated Multi-Country" :models="modelsEstimatedCalibratedMultiCountry"/>
                <ModelList name="Estimated Other Countries" :models="modelsEstimatedOtherCountries"/>
            </b-row>
        </div>
    </div>
</template>
<script>
  import ModelList from '@/components/ModelList.vue';
  import ModelSearch from '@/components/ModelSearch.vue';
  import { mapMutations, mapGetters, mapActions } from 'vuex'; // eslint-disable-line no-unused-vars

  export default {
    components: {
      ModelList,
      ModelSearch,
    },
    data() {
      return {};
    },
    computed: {
      ...mapGetters('models', [
        'total',
        'modelsCalibrated',
        'modelsEstimatedUs',
        'modelsEstimatedEuroArea',
        'modelsEstimatedCalibratedMultiCountry',
        'modelsEstimatedOtherCountries',
      ]),
      ...mapGetters('selections', {
        selectedIndex: 'numModels',
      }),
    },
    methods: {
      ...mapMutations('selections', ['clearModels']),
    },
  };
</script>