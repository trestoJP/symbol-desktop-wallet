<template>
    <div class="container">
        <Modal
            v-model="show"
            class-name="modal-transaction-confirmation"
            :title="$t('modal_title_transaction_confirmation')"
            :transfer="false"
            :footer-hide="true"
        >
            <div class="transactionConfirmationBody">
                <div v-if="!!stagedTransactions" class="stepItem1">
                    <div v-for="(transaction, index) in stagedTransactions" :key="index" class="info_container">
                        <TransactionDetails :transaction="transaction" />
                    </div>

                    <HardwareConfirmationButton v-if="isUsingHardwareWallet" @success="onSigner" @error="onError" />
                    <FormProfileUnlock v-else @success="onAccountUnlocked" @error="onError" />
                </div>
            </div>
        </Modal>
    </div>
</template>

<script lang="ts">
import { ModalTransactionConfirmationTs } from './ModalTransactionConfirmationTs';
export default class ModalTransactionConfirmation extends ModalTransactionConfirmationTs {}
</script>

<style lang="less" scoped>
@import '../../resources/css/variables.less';
.float-right {
    float: right;
}

.clear-staged-transactions {
    font-size: @smallFont;
    cursor: pointer;
}
</style>
