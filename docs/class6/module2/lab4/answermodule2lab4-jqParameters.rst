Answer Module 2 Lab 4 
======================

To get the parameters defined in a policy, fill in <policy id> which the ansible1 policy id

.. code-block:: bash

        curl -sk -u admin:$password -X GET https://10.1.1.245/mgmt/tm/asm/<policy id>/parameters | jq

|

The output should be similar to (output is truncated):

|

.. code-block:: json

        {
        "kind": "tm:asm:policies:parameters:parametercollectionstate",
        "selfLink": "https://localhost/mgmt/tm/asm/policies/u-6T62j_f0XMkjJ_s_Z-gg/parameters?ver=13.1.0",
        "totalItems": 441,
        "items": [
                {
                "isBase64": false,
                "checkMetachars": true,
                "dataType": "alpha-numeric",
                "lastLearnedNewEntityDatetime": "2018-05-21T04:30:22Z",
                "sensitiveParameter": false,
                "valueType": "user-input",
                "kind": "tm:asm:policies:parameters:parameterstate",
                "selfLink": "https://localhost/mgmt/tm/asm/policies/u-6T62j_f0XMkjJ_s_Z-gg/parameters/-5Mv4LmXybsPORDg7A4N0g?ver=13.1.0",
                "inClassification": false,
                "nameMetacharOverrides": [],
                "metacharsOnParameterValueCheck": true,
                "id": "-5Mv4LmXybsPORDg7A4N0g",
                "allowEmptyValue": true,
                "checkMaxValueLength": false,
                "valueMetacharOverrides": [],
                "name": "*pgsz*",
                "lastUpdateMicros": 1526877024000000,
                "allowRepeatedParameterName": false,
                "level": "global",
                "attackSignaturesCheck": true,
                "signatureOverrides": [],
                "performStaging": true,
                "type": "wildcard",
                "enableRegularExpression": false,
                "wildcardOrder": 27
                },

|

To go back to the previous page, please user your browser’s back button
