//# Netsuite_Suitescript_User-Event-Script
//Task1_enter the value on PO# field and set on the memo field once the user click on save button
/**
 * @NApiVersion 2.x
 * @NScriptType UserEventScript
 */
define(['N/record', 'N/log'], function(record, log) {

    function beforeSubmit(context) {
        try {
            var newRecord = context.newRecord;

            log.debug({
                title: 'Event Type',
                details: context.type
            });

            var poNumber = newRecord.getValue({
                fieldId: 'otherrefnum'
            });

            log.debug({
                title: 'PO Number',
                details: poNumber
            });

            if (poNumber) {
                newRecord.setValue({
                    fieldId: 'memo',
                    value: poNumber
                });
            }

        } catch (e) {
            log.error({
                title: 'Error in beforeSubmit',
                details: e
            });
        }
    }

    return {
        beforeSubmit: beforeSubmit
    };
});


This is an user event script