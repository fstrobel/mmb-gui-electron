<template>
    <div class="ctrl-set ctrl-set-prules">
        <div class="ctrl-set-header">
            <div class="ctrl-set-title">
                Policy Rules
                <small class="ctrl-set-stats">({{selectedIndex}}/{{rules.length}} Selected)</small>
                <a href="javascript:void(0)" class="ctrl-set-clear" @click="clear">&nbsp;Clear</a>
            </div>
        </div>

        <div class="ctrl-set-body">
            <b-form-checkbox-group class="ctrl-set-listing" stacked v-model="selection">
                <b-form-checkbox class="cb-user-rule" :key="1" :value="{ id: 1 }" :disabled="isRuleDisabled(1)">
                    User specified rule
                    <a href="javascript:void(0)" v-b-modal.userSpecifiedRuleModal>(edit)</a>
                </b-form-checkbox>
                <b-form-checkbox :key="2" :value="{ id: 2 }" :disabled="isRuleDisabled(2)">
                    <span class="rule-caption"
                          :style="{ opacity: isRuleDisabled(2) ? .5 : 1 }">Model specific rule</span>
                </b-form-checkbox>

                <template v-for="(rule, index) in rules">
                    <div :id="'cb-rule-' + rule.id">
                        <b-form-checkbox ref="cb" :value="rule" :disabled="isRuleDisabled(rule.id)">
                            {{ rule.description.ac_ref }}
                        </b-form-checkbox>

                    </div>
                    <RulePopover :rule="rule"/>
                </template>
            </b-form-checkbox-group>
        </div>
    </div>
</template>
<script>
  import { mapMutations, mapGetters } from 'vuex'; // eslint-disable-line no-unused-vars
  import RulePopover from './RulePopover';

  export default {
    components: {
      RulePopover,
    },
    computed: {
      ...mapGetters('rules', ['rules']),
      ...mapGetters('selections', {
        isRuleDisabled: 'isRuleDisabled',
        selectedIndex: 'numPolicyRules',
        policyRuleSelection: 'policyRules',
      }),
      selection: {
        get() {
          return this.policyRuleSelection;
        },
        set(value) {
          this.setPolicyRules(value);
        },
      },
    },
    methods: {
      ...mapMutations('selections', {
        clear: 'clearPolicyRules',
        setPolicyRules: 'setPolicyRules',
      }),
    },
  };
</script>
<style lang="scss">
    .cb-user-rule > label {
        display: flex !important;
        justify-content: space-between;
    }
</style>
<style scoped lang="scss">
    .rule-caption {
        transition: opacity .15s ease-in-out;
    }
</style>
