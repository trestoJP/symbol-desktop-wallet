<template>
    <FormWrapper>
        <ValidationObserver v-slot="{ handleSubmit }" ref="observer" slim>
            <form onsubmit="event.preventDefault()">
                <SignerSelector v-model="formItems.signerAddress" :signers="signers" @input="onChangeSigner" />

                <SupplyInput v-model="formItems.supply" />

                <DivisibilityInput v-model="formItems.divisibility" />

                <DurationInput
                    v-show="!formItems.permanent"
                    v-model="formItems.duration"
                    :show-relative-time="true"
                    target-asset="mosaic"
                />

                <FormRow>
                    <template v-slot:inputs>
                        <div class="inputs-container checkboxes">
                            <Checkbox v-model="formItems.permanent">
                                {{ $t('duration_permanent') }}
                            </Checkbox>
                            <Checkbox v-model="formItems.transferable">
                                {{ $t('transmittable') }}
                            </Checkbox>
                            <Checkbox v-model="formItems.supplyMutable">
                                {{ $t('variable_supply') }}
                            </Checkbox>
                            <Checkbox v-model="formItems.restrictable">
                                {{ $t('restrictable') }}
                            </Checkbox>
                        </div>
                    </template>
                </FormRow>
                <RentalFee :rental-type="'mosaic'"></RentalFee>
                <MaxFeeAndSubmit v-model="formItems.maxFee" @button-clicked="handleSubmit(onSubmit)" />
            </form>
        </ValidationObserver>

        <ModalTransactionConfirmation
            v-if="hasConfirmationModal"
            :command="command"
            :visible="hasConfirmationModal"
            @success="onConfirmationSuccess"
            @error="onConfirmationError"
            @close="onConfirmationCancel"
        />
    </FormWrapper>
</template>

<script lang="ts">
// @ts-ignore
import { FormMosaicDefinitionTransactionTs } from './FormMosaicDefinitionTransactionTs';
export default class FormMosaicDefinitionTransaction extends FormMosaicDefinitionTransactionTs {}
</script>

<style lang="less" scoped>
.checkboxes {
    display: grid;
    grid-auto-flow: column;
    align-items: baseline;
    color: #44004e;
}

/deep/ .form-row {
    .form-row-inner-container {
        grid-template-columns: 3rem 8rem;
    }
}
</style>
