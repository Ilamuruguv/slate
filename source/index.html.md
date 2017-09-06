---
title: API Reference

language_tabs: # must be one of https://git.io/vQNgJ
  - java 
  - other
  - shell
  - javascript

toc_footers:
  - 
  - 

includes:
  - errors

search: true
---

# Introduction

Welcome to the OCE API Documentation! You can use our API to access Order API endpoints, which can get information on various APIs from the OCE Application.

This example API documentation page was created with [Slate](https://github.com/tripit/slate).

# Authentication

> To authorize, use this code:

```java
	Header(s)
		X-APP-Bitmap 0000000000000001000000000000000000000000000001010000000000000000	
		Authorization Basic U0hBUkVEU0VSVklDRVM6U1RBUlRIUjMzUk9DS1M=
```

```other
	Header(s)
		X-APP-Bitmap 0000000000000001000000000000000000000000000001010000000000000000	
		Authorization Basic U0hBUkVEU0VSVklDRVM6U1RBUlRIUjMzUk9DS1M=
```

```shell
# With shell, you can just pass the correct header with each request
curl "api_endpoint_here"
  -H "Authorization: Basic U0hBUkVEU0VSVklDRVM6U1RBUlRIUjMzUk9DS1M="
  -H "X-APP-Bitmap: 0000000000000001000000000000000000000000000001010000000000000000"
```

```javascript
Header(s)
		X-APP-Bitmap 0000000000000001000000000000000000000000000001010000000000000000	
		Authorization Basic U0hBUkVEU0VSVklDRVM6U1RBUlRIUjMzUk9DS1M=
```


# Orders

## Post an order to OCE


### HTTP Request
`POST http://host:port/restservices/oce/v6/orders`


Parameter | Mandatory | Description
--------- | --------- | -----------
Order number | yes | Every order needs to be sent with the unique order no 

![postman](/images/postman.png) Please download the [Postman collection] (https://www.getpostman.com/collections/2aa708aa5350486de815) from this link.

1. Step 1
2. Step 2
3. Step 3
   * Item 3a
   * Item 3b
   * Item 3c
   

> Request BODY JSON structured like this:

```json

1. Step 1
2. Step 2
3. Step 3
   * Item 3a
   * Item 3b
   * Item 3c
   
{
	"oceBitMap": "0000000000000000000000000000000000000000000000100000000100110001",
	"version": "V11",
	"order": {
		"customerOrderNumber": "22-137578111080706",
		"orderType": "CREATE",
		"orderStatus": {
			"status": "RECEIVED"
		},
		"createdDate": 1503972660672,
		"submittedDate": 1503972660672,
		"productGroups": {
			"group": [{
				"id": "GROUP_01",
				"name": "UPGRADE_WIRELESS",
				"type": "LINE_OF_SERVICE",
				"sequence": 1,
				"price": [{
					"amount": 649.99,
					"currencyType": "USD",
					"priceType": "DueToday",
					"taxDetail": {
						"amount": 65
					},
					"total": 714.99
				}, {
					"amount": 0,
					"currencyType": "USD",
					"total": 0
				}, {
					"amount": 0,
					"currencyType": "USD",
					"priceType": "NRC",
					"total": 0
				}, {
					"amount": 0,
					"currencyType": "USD",
					"priceType": "DUENOW",
					"total": 0
				}],
				"characteristics": {
					"losgCharacteristics": {
						"losgReferenceId": "losg18040730",
						"sequence": 1,
						"losgType": "UP",
						"productCategory": "WIRELESS",
						"primaryIndicator": true,
						"dealerCode": "K3K6I",
						"market": "NWS",
						"subMarket": "PNW",
						"serviceArea": "006300008879",
						"priceCode": "PNW",
						"accountReference": "ACCOUNT_01",
						"serviceLocationReference": "ADDRESS_02",
						"wirelessLOSCharacteristics": {
							"mobileNumber": "2069792230",
							"upgradeQualificationDetails": [{
								"approvalNumber": "0",
								"newAEUCheckerIndicator": true
							}],
							"billingSystemId": "T"
						},
						"fulfillmentMethod": "DF",
						"shippingDetailReference": "SHIPPING_INFO_01"
					}
				}
			}]
		},
		"lineItems": {
			"lineItem": [{
				"id": "83993002267",
				"sequence": 1,
				"productCode": "prod8730224",
				"productSKU": "6474A",
				"billingCode": "6474A",
				"productType": "HARDGOOD",
				"displayName": "Apple iPhone 7 - 32GB - Gold",
				"systemName": "PHO APL IPHONE 7 32GB GLD",
				"action": "ADD",
				"price": {
					"amount": 649.99,
					"baseAmount": 0.0,
					"msrp": 649.99,
					"priceType": "DueToday",
					"taxDetail": {
						"preCalculatedTax": {
							"taxableCost": 649,
							"taxableMSRP": 0,
							"taxableUnitPrice": 649.99,
							"orderTaxAreaId": 390950000,
							"shipFromTaxAreaId": 431570560,
							"shipToTaxAreaId": 480331340
						},
						"lineItemTaxes": [{
							"taxLineId": 1,
							"taxCode": "SALESTAX",
							"memo": "SALESTAX",
							"printName": "Sales Tax",
							"taxable": "X",
							"skuSpecific": "false",
							"jurisdictionLevel": "Sales Tax",
							"jurisdictionName": "Sales Tax",
							"taxAmount": 65,
							"taxRate": 0.1,
							"taxDate": "2017-08-28"
						}]
					},
					"total": 714.99
				},
				"locationId": "K006",
				"payments": {
					"payment": [{
						"paymentOptionReference": "PAYMENT_OPTION_01"
					}]
				},
				"contractDetails": {
					"contractDisplayName": "",
					"installmentPlanDefinition": "regular",
					"totalSalePrice": 0.0,
					"installmentType": "PHONE",
					"contractType": "NOCOMMIT",
					"contractSystem": "OPTICAL",
					"contractSent": "N",
					"contractLength": 0
				},
				"quantity": 1,
				"groupReferences": {
					"groupReference": ["GROUP_01"]
				},
				"characteristics": {
					"wirelessLineItemCharacteristics": {
						"nciEligibleIndicator": false
					}
				},
				"hardGood": {
					"byodIndicator": false,
					"hardGoodType": "DEVICE",
					"productImageUrl": "https://tst04.stage.att.com/catalog/en/skus/images/apple-iphone 7-gold-100x160.png",
					"make": "Apple",
					"model": "iPhone 7",
					"shipmentCommitDate": {
						"fromDate": 1503964800000,
						"toDate": 1504137600000
					},
					"wirelessHardGoodCharacteristics": {
						"techType": "UMTS",
						"equipmentType": "EDGE",
						"imeiType": "J0",
						"phoneType": "ANY_PHONE",
						"deviceCategory": "SP"
					}
				}
			}, {
				"id": "83993002267-1",
				"sequence": 2,
				"productCode": "NOT_AVAILABLE",
				"productSKU": "84514",
				"billingCode": "84514",
				"productType": "HARDGOOD",
				"displayName": "Kit_guide_eCom_Phone_13.0",
				"systemName": "COL QSG GET STARTED CONSUMER SLIP",
				"action": "ADD",
				"price": {
					"amount": 0,
					"msrp": 0,
					"priceType": "DueToday",
					"taxDetail": {
						"preCalculatedTax": {
							"taxableCost": 0,
							"taxableMSRP": 0,
							"taxableUnitPrice": 0,
							"orderTaxAreaId": 390950000,
							"shipFromTaxAreaId": 431570560,
							"shipToTaxAreaId": 480331340
						},
						"lineItemTaxes": [{
							"taxLineId": 1,
							"taxCode": "SALESTAX",
							"memo": "SALESTAX",
							"printName": "Sales Tax",
							"taxable": "X",
							"skuSpecific": "false",
							"jurisdictionLevel": "Sales Tax",
							"jurisdictionName": "Sales Tax",
							"taxAmount": 0,
							"taxRate": 0,
							"taxDate": "2017-08-28"
						}]
					},
					"total": 0.0
				},
				"locationId": "K006",
				"payments": {
					"payment": [{
						"paymentOptionReference": "PAYMENT_OPTION_01"
					}]
				},
				"quantity": 1,
				"groupReferences": {
					"groupReference": ["GROUP_01"]
				},
				"hardGood": {
					"hardGoodType": "COLLATERAL"
				}
			}, {
				"id": "83993002267-2",
				"sequence": 3,
				"productCode": "NOT_AVAILABLE",
				"productSKU": "73023",
				"billingCode": "73023",
				"productType": "HARDGOOD",
				"displayName": "Embedded Nano SIM for iPhone 7, 7plus",
				"systemName": "Embedded SIM",
				"action": "ADD",
				"price": {
					"amount": 0,
					"msrp": 0,
					"priceType": "DueToday",
					"taxDetail": {
						"preCalculatedTax": {
							"taxableCost": 0,
							"taxableMSRP": 0,
							"taxableUnitPrice": 0,
							"orderTaxAreaId": 390950000,
							"shipFromTaxAreaId": 431570560,
							"shipToTaxAreaId": 480331340
						},
						"lineItemTaxes": [{
							"taxLineId": 1,
							"taxCode": "SALESTAX",
							"memo": "SALESTAX",
							"printName": "Sales Tax",
							"taxable": "X",
							"skuSpecific": "false",
							"jurisdictionLevel": "Sales Tax",
							"jurisdictionName": "Sales Tax",
							"taxAmount": 0,
							"taxRate": 0,
							"taxDate": "2017-08-28"
						}]
					},
					"total": 0.0
				},
				"locationId": "K006",
				"payments": {
					"payment": [{
						"paymentOptionReference": "PAYMENT_OPTION_01"
					}]
				},
				"quantity": 1,
				"groupReferences": {
					"groupReference": ["GROUP_01"]
				},
				"hardGood": {
					"hardGoodType": "SIM"
				}
			}, {
				"id": "83993002267-5",
				"sequence": 4,
				"productCode": "NOT_AVAILABLE",
				"productSKU": "NOT_AVAILABLE",
				"billingCode": "NOT_AVAILABLE",
				"productType": "MISC_CHARGE",
				"displayName": "Upgrade Fee",
				"systemName": "UPGRADE_FEE",
				"action": "ADD",
				"price": {
					"amount": 0,
					"msrp": 0,
					"priceType": "NRC"
				},
				"locationId": "K006",
				"payments": {
					"payment": [{
						"paymentOptionReference": "PAYMENT_OPTION_01"
					}]
				},
				"quantity": 0,
				"groupReferences": {
					"groupReference": ["GROUP_01"]
				}
			}, {
				"id": "88879ShippingFee",
				"sequence": 5,
				"productCode": "NOT_AVAILABLE",
				"productSKU": "88879",
				"billingCode": "88879",
				"productType": "MISC_CHARGE",
				"displayName": "ShippingFee",
				"systemName": "SHIPPING_FEE",
				"action": "ADD",
				"price": {
					"amount": 0,
					"priceType": "DueToday",
					"taxDetail": {
						"preCalculatedTax": {
							"taxableCost": 0,
							"taxableMSRP": 14.95,
							"taxableUnitPrice": 0,
							"orderTaxAreaId": 390950000,
							"shipFromTaxAreaId": 431570560,
							"shipToTaxAreaId": 480331340
						},
						"lineItemTaxes": [{
							"taxLineId": 1,
							"taxCode": "SALESTAX",
							"memo": "SALESTAX",
							"printName": "Sales Tax",
							"taxable": "X",
							"skuSpecific": "false",
							"jurisdictionLevel": "Sales Tax",
							"jurisdictionName": "Sales Tax",
							"taxAmount": 0,
							"taxRate": 0,
							"taxDate": "2017-08-28"
						}]
					},
					"total": 0
				},
				"payments": {
					"payment": [{
						"paymentOptionReference": "PAYMENT_OPTION_01"
					}]
				},
				"quantity": 1,
				"groupReferences": {
					"groupReference": ["GROUP_01"]
				}
			}]
		},
		"names": {
			"name": [{
				"id": "NAME_01",
				"firstName": "BEDROCK",
				"lastName": "DONOTUSE",
				"emailAddress": "sa240y@ATT.COM",
				"primaryContactPhones": [{
					"phoneNumber": "4252887410",
					"contactPhoneType": "HOME_PHONE"
				}]
			}]
		},
		"addresses": {
			"address": [{
				"id": "ADDRESS_01",
				"unparsedAddress": {
					"addressLine1": "20307 N CREEK PKWY",
					"city": "BOTHELL",
					"state": "WA",
					"zip": "98011",
					"country": "US"
				},
				"additionalDetails": {
					"additionalDetail": [{
						"code": "ValidatedAddress",
						"value": "true"
					}]
				}
			}, {
				"id": "ADDRESS_02",
				"addressId": "ADDRESS_02",
				"unparsedAddress": {
					"addressLine1": "20307 N CREEK PKWY",
					"city": "BOTHELL",
					"state": "WA",
					"zip": "98011",
					"country": "US"
				},
				"additionalDetails": {
					"additionalDetail": [{
						"code": "ValidatedAddress",
						"value": "true"
					}]
				}
			}]
		},
		"accounts": {
			"account": [{
				"id": "ACCOUNT_01",
				"sequence": 1,
				"accountCategory": "MOBILITY_ACCOUNT",
				"accountSubCategory": "EXISTING",
				"paymentArrangement": "POSTPAID",
				"billingAccountNumber": "512127125265",
				"billingDetail": [{
					"nameReference": "NAME_01",
					"addressReference": "ADDRESS_01",
					"authentication": {
						"dob": "_4TZ-2p-Ll",
						"driversLicense": {},
						"ssn": "B1VK4RRYQ"
					},
					"previousAddress": "N"
				}],
				"creditCheck": {
					"creditCheckRanIndicator": false
				},
				"liabilityType": "INDIVIDUAL",
				"accountType": "INDIVIDUAL",
				"accountSubType": "R",
				"enterpriseType": "IRU",
				"b2bReference": "B2B_01",
				"langId": "ENGLISH",
				"market": "NWS",
				"subMarket": "PNW",
				"spokenLanguagePreference": "ENGLISH"
			}]
		},
		"paymentOptions": {
			"paymentOption": [{
				"id": "PAYMENT_OPTION_01",
				"sequence": 1,
				"capmConfig": {
					"merchantId": "ORDERGWCon",
					"sourceSystem": "HARDROCK",
					"sourceLocation": "CS",
					"sourceUser": "HARDROCK"
				},
				"paymentMethod": {
					"capm": {
						"preAuthDetail": {
							"authorizationCode": "OL_DF170828P01271",
							"authorizationDate": "2017-08-28",
							"authorizationExpirationDate": "2017-09-25",
							"addressVerificationSystemCode": "NA",
							"authorizationKey": "40420967"
						},
						"totalAmount": 714.99,
						"creditCardLast4Digits": "2784",
						"zipCode": "98011",
						"creditCardType": "MASTERCARD",
						"paymentProfileAction": "C_ORDER",
						"giftCardIndicator": false
					}
				}
			}]
		},
		"shippingDetails": {
			"shippingDetail": [{
				"id": "SHIPPING_INFO_01",
				"sequence": 1,
				"nameReference": "NAME_01",
				"addressReference": "ADDRESS_01",
				"shippingCode": "F1",
				"shippingPriceCode": "88879",
				"shippingMethod": "Overnight",
				"carrierPreference": "FedEx"
			}]
		},
		"b2bs": {
			"b2b": [{
				"id": "B2B_01",
				"b2bContractProvider": "ATTWS",
				"b2bContractType": "CBE",
				"b2bFAN": "00030561",
				"b2bSkipUpgradeEligibilityIndicator": false,
				"b2bIgnoreDepositRequiredIndicator": false,
				"b2bFANBusinessName": "DEMO TEST FAN"
			}]
		},
		"totalPrice": {
			"price": [{
				"amount": 649.99,
				"currencyType": "USD",
				"priceType": "DueToday",
				"taxDetail": {
					"amount": 65
				},
				"total": 714.99
			}, {
				"amount": 0,
				"currencyType": "USD",
				"priceType": "RC",
				"total": 0
			}, {
				"amount": 0,
				"currencyType": "USD",
				"priceType": "NRC",
				"total": 0
			}, {
				"amount": 0,
				"currencyType": "USD",
				"priceType": "DUENOW",
				"total": 0
			}]
		},
		"creditPolicy": {
			"crsmOnFlag": false
		},
		"agentCode": "K3K6I",
		"agentLocation": "K3K6I",
		"orderContact": {
			"nameReference": "NAME_01",
			"primaryEmailAddress": "sa240y@ATT.COM"
		},
		"salesChannel": "E",
		"orderSource": {
			"locale": "en_US",
			"clientType": "DESKTOP",
			"channel": "DE-MOBILITY",
			"application": "MYATTSALES",
			"browserId": "A001295391884",
			"additionalDetails": {
				"additionalDetail": [{
					"code": "ORDER_STATUS_URL",
					"value": "https://opss-qa2.stage.att.com/checkmyorder/processOSRequest.rt?onum=22-137578111080706&appid=OCE&isCRU=false&context=56NshdhRd6dJkIm%2F3VovBzMkCA9ar7Vz%2BNH7GhPrQMCOBYDuSBOgyylxPvbSMYdm%2BFDk1KhZv3Np7PgnMwydtgXsLfm%2Be02ASjCf39Ays1itpMbhYA1n6stOyJS13%2BZGZSIzP%2FbXR9PAGWU8Cm5iQeRU9aM%2BCyCXhceh7Qk5kI2XQAOMIIUukPUbQuuqn5USUskoXIsao%2BUl6VNK9BVW1tAIgxsIwPbiXonlFqcRWcNukJ4TVfRtM5%2FIoQfpDgkoHTAIH%2F2ToZVONRsXBfrLMIcP%2BYlwUIDYj0qwXvgLS%2FVhVppaFNhkL4NROyVEs6tFZrDFk8RDeETRUNLePgmvttXQ6wkIjl5dRw0dfm8feInDG%2FCzWLSvB7nheg5IChy5yMHuYr6m3xd0M%2FhltsneSNeSuSc6%2F07WYR0NZT565wdNwxCCSQayhGJe5WQz7ub%2FrKRA2q34gueqprBAPkQUK6dfdaONNE9ffEV%2Bh24yhBwL51%2FP6%2FeP3Hi2xBHx1wDqrwPpcJaBV89UW%2BJZIJUtEEc9KddB8Bi1rZNf4VmcK1lYCPm08MuZ4FLcxFl32C1G"
				}, {
					"code": "SENDER",
					"value": "CCC_Zippy"
				}]
			}
		},
		"encryptedIndicator": true,
		"commonOrderIndicator": true,
		"summaryCreatedIndicator": false,
		"requestId": "f9522be6-d882-4511-977e-1ac62a3660cd"
	}
}	
```

> The above command returns JSON structured like this:

```json
{
  "application": "MYATTSALES",
  "channel": "DE-MOBILITY",
  "customerOrderNumber": "22-137578111080706"
}
```

## Retrieve an order from OCE


### HTTP Request  to retrieve the order by BAN

`GET http://host:port/restservice/inquire?[ban][ctn]=1234567891`

### Query Parameters

Parameter | Default | Description
--------- | ------- | -----------
BAN/CTN  | yes | BAN/CTN no of the order

> The above command returns JSON structured like this:

```json
{
  "MetaInformation": null,
  "OrderDetails": [
    {
      "CurrentDateTime": 1504115790918,
      "EmailMsg": null,
      "Errors": {},
      "Order": {
        "AcceptedDate": 1504064563108,
        "Accounts": {
          "Account": [
            {
              "AccountCategory": "MOBILITY_ACCOUNT",
              "AccountCrossmarketIndicator": false,
              "AccountSequenceNumber": 1,
              "AccountSubCategory": "EXISTING",
              "AccountSubType": "L",
              "AccountType": "GOVERNMENT",
              "B2BRef": "B2B_01",
              "BankingPartner": {},
              "BillingAccountNumber": "999253500",
              "BillingDeliveryPreference": "PAPER",
              "BillingInfo": [
                {
                  "AccountStatus": "ACTIVE",
                  "AddressRef": "ADDRESS_01",
                  "Authentication": {
                    "DriversLicense": {},
                    "EmployerInfo": {},
                    "SSNRefusedIndicator": true,
                    "SecurityVerification": {},
                    "StateId": {}
                  },
                  "NameRef": "NAME_02"
                }
              ],
              "BillingLanguagePreference": "ENGLISH",
              "CTNValidated": false,
              "ConsentToCC": false,
              "ContractAcceptance": {},
              "CreditAlert": {},
              "CreditCheck": {
                "CCRan": false
              },
              "DelinquentAccount": false,
              "ELOA": {},
              "EnterpriseType": "GBS",
              "Id": "ACCOUNT_01",
              "LangId": "ENGLISH",
              "LiabilityType": "CORPORATE",
              "Market": "NBI",
              "MdmProfileSetting": {},
              "PaymentArrangement": "POSTPAID",
              "PriceCode": "SAC",
              "ProvisioningSystems": {},
              "SpokenLanguagePreference": "ENGLISH",
              "SubMarket": "SAC",
              "UnifiedAccount": {
                "ConvergeOrder": false,
                "ConvergeValidation": false,
                "PremierIndicator": false
              }
            }
          ]
        },
        "AdditionalDetails": {
          "AdditionalDetail": [
            {
              "Code": "PRODUCT_COMBINATION",
              "Type": "Order",
              "Value": "WIRELESS_AL"
            }
          ]
        },
        "Addresses": {
          "Address": [
            {
              "Id": "ADDRESS_01",
              "ParsedAddress": {},
              "UnparsedAddress": {
                "AddressLine1": "2315 Stockton Blvd",
                "AddressLine2": "ASB 2120",
                "Attention": "Telecommunications",
                "City": "Sacramento",
                "Country": "US",
                "State": "CA",
                "Zip": "95817"
              }
            },
            {
              "Id": "ADDRESS_02",
              "ParsedAddress": {},
              "UnparsedAddress": {
                "AddressLine1": "UC Davis Medical Center",
                "AddressLine2": "2450 48th Street Rm 1820",
                "Attention": "John Raygoza",
                "City": "Sacramento",
                "Country": "US",
                "State": "CA",
                "Zip": "95817"
              }
            },
            {
              "Id": "ADDRESS_03",
              "ParsedAddress": {},
              "UnparsedAddress": {
                "AddressLine1": "2315 Stockton Blvd.",
                "Attention": "NOT_AVAILABLE",
                "City": "Sacramento",
                "Country": "US",
                "State": "CA",
                "Zip": "95817"
              }
            }
          ]
        },
        "AgentCode": "6F728",
        "AgentLocation": "Z0066",
        "ApproverNameRefs": {},
        "B2Bs": {
          "B2B": [
            {
              "B2BContractProvider": "ATTWS",
              "B2BContractType": "WSCA",
              "B2BFAN": "00061007",
              "B2BFANBusinessName": "UC DAVIS FACULTY & STAFF\n\t\t\t\t",
              "B2BIgnoreDepositRequired": true,
              "B2BSalesRepCode": "ic6f728",
              "B2BskipUpgradeEligibility": false,
              "CompanyName": "UC DAVIS FACULTY & STAFF",
              "ExemptOrderId": "N05000480",
              "Id": "B2B_01",
              "ManageCallListReferences": {},
              "TaxExemptInd": true
            }
          ]
        },
        "CreatedDate": 1503959356000,
        "CurrentDateTime": 1504115788435,
        "CustomerOrderNumber": "22-137578111080706",
        "DueAmount": {
          "Amount": 162.99,
          "CurrencyType": "USD",
          "PriceType": "DueToday",
          "TaxInfo": {
            "Amount": 50.57
          },
          "Total": 213.56
        },
        "ExternalOrderSource": "PRE",
        "Groups": {
          "Group": [
            {
              "GroupCharacteristics": {
                "LoSGCharacteristics": {
                  "ADDPLOSChars": {},
                  "AccountRef": "ACCOUNT_01",
                  "CommonLOSCharacteristics": {},
                  "Compensation": {},
                  "ConflictingServiceInfoRefs": {},
                  "DealerCode": "6F728",
                  "DirecTVLOSChars": {},
                  "FulfillmentMethod": "DF",
                  "InstallationInstructions": {},
                  "InternetLOSChars": {},
                  "IsAutomationEnabled": false,
                  "IsPrimary": false,
                  "LoSGReferenceId": "losg136762526216002",
                  "LoSGSequenceNumber": 1,
                  "LoSGStatus": {
                    "Status": "IN_QUEUE",
                    "SubStatus": "FRAUD_REVIEW_MED"
                  },
                  "LoSGType": "AL",
                  "Market": "NBI",
                  "NumberPortInfo": {
                    "DisconnectAcknowledged": {}
                  },
                  "PreferredAreaCode": "916",
                  "PriceCode": "SAC",
                  "ProductCategory": "WIRELESS",
                  "ServiceArea": "008304008580",
                  "ServiceAreaName": "Sacramento CA (916)",
                  "ServiceLocationRef": "ADDRESS_03",
                  "ShippingInfoRef": "SHIPPING_INFO_01",
                  "SubMarket": "SAC",
                  "SubscriberNameRef": "NAME_04",
                  "TCAccepted": {},
                  "TCRefs": {},
                  "VOIPLOSChars": {},
                  "WirelessLOSChars": {
                    "BillingSystemId": "NBI",
                    "ConnectedCarInfo": {},
                    "IsCrossUpgrade": false,
                    "IsPrimarySharedPlan": false,
                    "ManageCallListReferences": {},
                    "PreOrder": false,
                    "UpgradeInfo": {}
                  }
                }
              },
              "Id": "GROUP_01",
              "Name": "NEW_WIRELESS",
              "Price": [
                {
                  "Amount": 162.99,
                  "CurrencyType": "USD",
                  "InstallmentEligibility": "N",
                  "PriceType": "DueToday",
                  "TaxInfo": {
                    "Amount": 50.57,
                    "LineItemTax": [
                      {
                        "JurisdictionLevel": "Sales Tax",
                        "JurisdictionName": "Sales Tax",
                        "Memo": "SALESTAX",
                        "SKUSpecificIndicator": "false",
                        "TaxAmount": 50.57,
                        "TaxCode": "SALESTAX",
                        "TaxDate": 1503878400000,
                        "TaxLineID": 1,
                        "TaxRate": 0.0825,
                        "TaxableIndicator": "X"
                      }
                    ]
                  },
                  "Total": 213.56
                }
              ],
              "Sequence": 1,
              "Type": "LINE_OF_SERVICE"
            }
          ]
        },
        "IsBulk": false,
        "IsCommonOrder": true,
        "IsEncrypted": false,
        "IsExpressCheckOut": false,
        "IsLocked": false,
        "IsPassThrough": false,
        "IsSummaryCreated": false,
        "LineItems": {
          "LineItem": [
            {
              "Action": "ADD",
              "BillingCode": "NOT_AVAILABLE",
              "Characteristics": {
                "AddOnSolutionCharacterstics": {},
                "CommonCharacteristics": {},
                "InternetLineItemChars": {},
                "VOIPLineItemChars": {},
                "WirelessLineItemChars": {
                  "ADTM": {},
                  "PDP": {},
                  "TradeInInfo": {}
                }
              },
              "DisplayName": "SHIPPING_FEE",
              "GroupRefs": {
                "GroupRef": [
                  "GROUP_01"
                ]
              },
              "Id": "SHIPPING_FEE",
              "LineItemSequence": 18,
              "Payments": {
                "Payment": [
                  {
                    "Amount": 0,
                    "CurrencyType": "USD",
                    "NoOfInstallment": 0,
                    "PaymentOptionRef": "PAYMENT_OPTION_01"
                  }
                ]
              },
              "Price": {
                "Amount": 0,
                "CurrencyType": "USD",
                "PriceType": "DueToday",
                "TaxInfo": {
                  "Amount": 0,
                  "LineItemTax": [
                    {
                      "JurisdictionLevel": "Sales Tax",
                      "JurisdictionName": "Sales Tax",
                      "Memo": "SALESTAX",
                      "SKUSpecificIndicator": "false",
                      "TaxAmount": 0,
                      "TaxCode": "SALESTAX",
                      "TaxDate": 1503878400000,
                      "TaxLineID": 1,
                      "TaxRate": 0,
                      "TaxableIndicator": "X"
                    }
                  ]
                },
                "Total": 0
              },
              "ProductCode": "WIRELESS_1",
              "ProductSku": "88888",
              "ProductType": "MISC_CHARGE",
              "Quantity": 1,
              "SupplyChainInfo": {},
              "SystemName": "SHIPPING_FEE"
            },
            {
              "Action": "ADD",
              "BillingCode": "NOT_AVAILABLE",
              "Characteristics": {
                "AddOnSolutionCharacterstics": {},
                "CommonCharacteristics": {},
                "InternetLineItemChars": {},
                "VOIPLineItemChars": {},
                "WirelessLineItemChars": {
                  "ADTM": {},
                  "PDP": {},
                  "TradeInInfo": {}
                }
              },
              "DisplayName": "Welcome Letter",
              "GroupRefs": {
                "GroupRef": [
                  "GROUP_01"
                ]
              },
              "HardGood": {
                "HardGoodType": "COLLATERAL",
                "IsShippedHot": true,
                "Make": "NOT_AVAILABLE",
                "PreOrder": false,
                "WirelessHardGoodChars": {}
              },
              "Id": "losg136762526216002_84515",
              "LineItemSequence": 19,
              "LocationID": "K008",
              "Payments": {
                "Payment": [
                  {
                    "Amount": 0,
                    "CurrencyType": "USD",
                    "NoOfInstallment": 0,
                    "PaymentOptionRef": "PAYMENT_OPTION_01"
                  }
                ]
              },
              "Price": {
                "Amount": 0,
                "CurrencyType": "USD",
                "InstallmentEligibility": "N",
                "PriceType": "DueToday",
                "TaxInfo": {
                  "Amount": 0,
                  "LineItemTax": [
                    {
                      "JurisdictionLevel": "Sales Tax",
                      "JurisdictionName": "Sales Tax",
                      "Memo": "SALESTAX",
                      "SKUSpecificIndicator": "false",
                      "TaxAmount": 0,
                      "TaxCode": "SALESTAX",
                      "TaxDate": 1503878400000,
                      "TaxLineID": 1,
                      "TaxRate": 0,
                      "TaxableIndicator": "X"
                    }
                  ]
                },
                "Total": 0
              },
              "ProductCode": "WIRELESS_2",
              "ProductSku": "84515",
              "ProductType": "HARDGOOD",
              "Quantity": 1,
              "SupplyChainInfo": {},
              "SystemName": "Welcome Letter"
            },
            {
              "Action": "ADD",
              "BillingCode": "NOT_AVAILABLE",
              "Characteristics": {
                "AddOnSolutionCharacterstics": {},
                "CommonCharacteristics": {},
                "InternetLineItemChars": {},
                "VOIPLineItemChars": {},
                "WirelessLineItemChars": {
                  "ADTM": {},
                  "PDP": {},
                  "TradeInInfo": {}
                }
              },
              "DisplayName": "COL SIG PROGRAM",
              "GroupRefs": {
                "GroupRef": [
                  "GROUP_01"
                ]
              },
              "HardGood": {
                "HardGoodType": "COLLATERAL",
                "IsShippedHot": true,
                "Make": "NOT_AVAILABLE",
                "PreOrder": false,
                "WirelessHardGoodChars": {}
              },
              "Id": "losg136762526216002_84637",
              "LineItemSequence": 20,
              "LocationID": "K008",
              "Payments": {
                "Payment": [
                  {
                    "Amount": 0,
                    "CurrencyType": "USD",
                    "NoOfInstallment": 0,
                    "PaymentOptionRef": "PAYMENT_OPTION_01"
                  }
                ]
              },
              "Price": {
                "Amount": 0,
                "CurrencyType": "USD",
                "InstallmentEligibility": "N",
                "PriceType": "DueToday",
                "TaxInfo": {
                  "Amount": 0,
                  "LineItemTax": [
                    {
                      "JurisdictionLevel": "Sales Tax",
                      "JurisdictionName": "Sales Tax",
                      "Memo": "SALESTAX",
                      "SKUSpecificIndicator": "false",
                      "TaxAmount": 0,
                      "TaxCode": "SALESTAX",
                      "TaxDate": 1503878400000,
                      "TaxLineID": 1,
                      "TaxRate": 0,
                      "TaxableIndicator": "X"
                    }
                  ]
                },
                "Total": 0
              },
              "ProductCode": "WIRELESS_3",
              "ProductSku": "84637",
              "ProductType": "HARDGOOD",
              "Quantity": 1,
              "SupplyChainInfo": {},
              "SystemName": "COL SIG PROGRAM"
            },
            {
              "Action": "ADD",
              "BillingCode": "NOT_AVAILABLE",
              "Characteristics": {
                "AddOnSolutionCharacterstics": {},
                "CommonCharacteristics": {},
                "InternetLineItemChars": {},
                "VOIPLineItemChars": {},
                "WirelessLineItemChars": {
                  "ADTM": {},
                  "PDP": {},
                  "TradeInInfo": {}
                }
              },
              "DisplayName": "Apple",
              "GroupRefs": {
                "GroupRef": [
                  "GROUP_01"
                ]
              },
              "HardGood": {
                "HardGoodType": "SIM",
                "IsShippedHot": true,
                "Make": "NOT_AVAILABLE",
                "PreOrder": false,
                "WirelessHardGoodChars": {}
              },
              "Id": "losg136762526216002_73023",
              "LineItemSequence": 21,
              "LocationID": "K008",
              "Payments": {
                "Payment": [
                  {
                    "Amount": 0,
                    "CurrencyType": "USD",
                    "NoOfInstallment": 0,
                    "PaymentOptionRef": "PAYMENT_OPTION_01"
                  }
                ]
              },
              "Price": {
                "Amount": 0,
                "CurrencyType": "USD",
                "InstallmentEligibility": "N",
                "PriceType": "DueToday",
                "TaxInfo": {
                  "Amount": 0,
                  "LineItemTax": [
                    {
                      "JurisdictionLevel": "Sales Tax",
                      "JurisdictionName": "Sales Tax",
                      "Memo": "SALESTAX",
                      "SKUSpecificIndicator": "false",
                      "TaxAmount": 0,
                      "TaxCode": "SALESTAX",
                      "TaxDate": 1503878400000,
                      "TaxLineID": 1,
                      "TaxRate": 0,
                      "TaxableIndicator": "X"
                    }
                  ]
                },
                "Total": 0
              },
              "ProductCode": "WIRELESS_4",
              "ProductSku": "73023",
              "ProductType": "HARDGOOD",
              "Quantity": 1,
              "SupplyChainInfo": {},
              "SystemName": "Apple"
            },
            {
              "Action": "ADD",
              "BillingCode": "NOT_AVAILABLE",
              "Characteristics": {
                "AddOnSolutionCharacterstics": {},
                "CommonCharacteristics": {},
                "InternetLineItemChars": {},
                "VOIPLineItemChars": {},
                "WirelessLineItemChars": {
                  "ADTM": {},
                  "PDP": {},
                  "TradeInInfo": {}
                }
              },
              "ContractDetails": {
                "AmountFinanced": 0,
                "AnnualPercentageRate": 0,
                "BalancedAmount": 0,
                "ContractDisplayName": "2Y",
                "ContractLength": 24,
                "ContractType": "REGULAR",
                "DownPayment": 0,
                "DownPaymentPercent": 0,
                "FinanceCharge": 0,
                "InstallmentAmount": 0,
                "InstallmentPlanID": 0,
                "IsEIP": false,
                "PrepaidFinanceCharge": 0,
                "TotalSalePrice": 0
              },
              "DisplayName": "Apple iPhone 6s (32GB Space Gray)",
              "GroupRefs": {
                "GroupRef": [
                  "GROUP_01"
                ]
              },
              "HardGood": {
                "BYOD": false,
                "HardGoodType": "DEVICE",
                "IsShippedHot": true,
                "Make": "Apple",
                "Model": "iPhone 6s A1633",
                "PreOrder": false,
                "ProductImageUrl": "https://wireless.att.com/business/images/equip/devices/iphone6s_gray_m.jpg\n\t\t\t\t\t",
                "ShipmentCommitDate": {
                  "FromDate": 1503979200000,
                  "ToDate": 1504152000000
                },
                "WirelessHardGoodChars": {
                  "EquipmentType": "GPRS",
                  "ImeiType": "K3",
                  "PhoneType": "HANDSET",
                  "TechType": "GSM"
                }
              },
              "Id": "alcitem24184616361802",
              "LineItemSequence": 1,
              "LocationID": "K008",
              "Payments": {
                "Payment": [
                  {
                    "Amount": 145.36,
                    "CurrencyType": "USD",
                    "PaymentOptionRef": "PAYMENT_OPTION_01"
                  }
                ]
              },
              "Price": {
                "Amount": 99.99,
                "CurrencyType": "USD",
                "InstallmentEligibility": "N",
                "MSRP": 549.99,
                "PriceType": "DueToday",
                "TaxInfo": {
                  "Amount": 45.37,
                  "LineItemTax": [
                    {
                      "JurisdictionLevel": "Sales Tax",
                      "JurisdictionName": "Sales Tax",
                      "Memo": "SALESTAX",
                      "SKUSpecificIndicator": "false",
                      "TaxAmount": 45.37,
                      "TaxCode": "SALESTAX",
                      "TaxDate": 1503878400000,
                      "TaxLineID": 1,
                      "TaxRate": 0.0825,
                      "TaxableIndicator": "X"
                    }
                  ]
                },
                "Total": 145.36
              },
              "ProductCode": "WIRELESS_5",
              "ProductSku": "6978A",
              "ProductType": "HARDGOOD",
              "Quantity": 1,
              "SupplyChainInfo": {},
              "SystemName": "Apple iPhone 6s (32GB Space Gray)"
            },
            {
              "Action": "ADD",
              "BillingCode": "NOT_AVAILABLE",
              "Characteristics": {
                "AddOnSolutionCharacterstics": {},
                "CommonCharacteristics": {},
                "InternetLineItemChars": {},
                "VOIPLineItemChars": {},
                "WirelessLineItemChars": {
                  "ADTM": {},
                  "PDP": {},
                  "TradeInInfo": {}
                }
              },
              "DisplayName": "OtterBox Defender Series Case",
              "GroupRefs": {
                "GroupRef": [
                  "GROUP_01"
                ]
              },
              "HardGood": {
                "HardGoodType": "ACCESSORY",
                "IsShippedHot": true,
                "Make": "NOT_AVAILABLE",
                "Model": "Cases",
                "PreOrder": false,
                "ProductImageUrl": "https://wireless.att.com/business/images/equip/accessories/4902F_s.jpg\n\t\t\t\t\t",
                "WirelessHardGoodChars": {}
              },
              "Id": "alcitem24184616321847",
              "LineItemSequence": 2,
              "LocationID": "K008",
              "Payments": {
                "Payment": [
                  {
                    "Amount": 37.89,
                    "CurrencyType": "USD",
                    "PaymentOptionRef": "PAYMENT_OPTION_01"
                  }
                ]
              },
              "Price": {
                "Amount": 35,
                "CurrencyType": "USD",
                "InstallmentEligibility": "N",
                "MSRP": 50,
                "PriceType": "DueToday",
                "TaxInfo": {
                  "Amount": 2.89,
                  "LineItemTax": [
                    {
                      "JurisdictionLevel": "Sales Tax",
                      "JurisdictionName": "Sales Tax",
                      "Memo": "SALESTAX",
                      "SKUSpecificIndicator": "false",
                      "TaxAmount": 2.89,
                      "TaxCode": "SALESTAX",
                      "TaxDate": 1503878400000,
                      "TaxLineID": 1,
                      "TaxRate": 0.0825,
                      "TaxableIndicator": "X"
                    }
                  ]
                },
                "Total": 37.89
              },
              "ProductCode": "WIRELESS_6",
              "ProductSku": "4902F",
              "ProductType": "HARDGOOD",
              "PromotionRefs": {
                "PromotionRef": [
                  "PROMOTION_01"
                ]
              },
              "Quantity": 1,
              "SupplyChainInfo": {},
              "SystemName": "OtterBox Defender Series Case"
            },
            {
              "Action": "ADD",
              "BillingCode": "NOT_AVAILABLE",
              "Characteristics": {
                "AddOnSolutionCharacterstics": {},
                "CommonCharacteristics": {},
                "InternetLineItemChars": {},
                "VOIPLineItemChars": {},
                "WirelessLineItemChars": {
                  "ADTM": {},
                  "PDP": {},
                  "TradeInInfo": {}
                }
              },
              "DisplayName": "OtterBox Symmetry Series Case",
              "GroupRefs": {
                "GroupRef": [
                  "GROUP_01"
                ]
              },
              "HardGood": {
                "HardGoodType": "ACCESSORY",
                "IsShippedHot": true,
                "Make": "NOT_AVAILABLE",
                "Model": "Cases",
                "PreOrder": false,
                "ProductImageUrl": "https://wireless.att.com/business/images/equip/accessories/4009G_s.jpg\n\t\t\t\t\t",
                "WirelessHardGoodChars": {}
              },
              "Id": "alcitem24184615711604",
              "LineItemSequence": 3,
              "LocationID": "K008",
              "Payments": {
                "Payment": [
                  {
                    "Amount": 30.31,
                    "CurrencyType": "USD",
                    "PaymentOptionRef": "PAYMENT_OPTION_01"
                  }
                ]
              },
              "Price": {
                "Amount": 28,
                "CurrencyType": "USD",
                "InstallmentEligibility": "N",
                "MSRP": 40,
                "PriceType": "DueToday",
                "TaxInfo": {
                  "Amount": 2.31,
                  "LineItemTax": [
                    {
                      "JurisdictionLevel": "Sales Tax",
                      "JurisdictionName": "Sales Tax",
                      "Memo": "SALESTAX",
                      "SKUSpecificIndicator": "false",
                      "TaxAmount": 2.31,
                      "TaxCode": "SALESTAX",
                      "TaxDate": 1503878400000,
                      "TaxLineID": 1,
                      "TaxRate": 0.0825,
                      "TaxableIndicator": "X"
                    }
                  ]
                },
                "Total": 30.31
              },
              "ProductCode": "WIRELESS_7",
              "ProductSku": "4009G",
              "ProductType": "HARDGOOD",
              "PromotionRefs": {
                "PromotionRef": [
                  "PROMOTION_01"
                ]
              },
              "Quantity": 1,
              "SupplyChainInfo": {},
              "SystemName": "OtterBox Symmetry Series Case"
            },
            {
              "Action": "ADD",
              "BillingCode": "MUOP",
              "Characteristics": {
                "AddOnSolutionCharacterstics": {},
                "CommonCharacteristics": {},
                "InternetLineItemChars": {},
                "VOIPLineItemChars": {},
                "WirelessLineItemChars": {
                  "ADTM": {},
                  "OfferType": "P",
                  "PDP": {},
                  "TradeInInfo": {}
                }
              },
              "DisplayName": "[discontinued] Multimedia Messaging Pay Per Use\n\t\t\t\t",
              "GroupRefs": {
                "GroupRef": [
                  "GROUP_01"
                ]
              },
              "Id": "losg136762526216002_sku89870382",
              "LineItemSequence": 22,
              "Payments": {},
              "Price": {
                "Amount": 0,
                "CurrencyType": "USD",
                "PriceType": "RC",
                "TaxInfo": {
                  "Amount": 0
                },
                "Total": 0
              },
              "ProductCode": "WIRELESS_9",
              "ProductSku": "NOT_AVAILABLE",
              "ProductType": "INCLUDED_FEATURE",
              "Quantity": 1,
              "SupplyChainInfo": {},
              "SystemName": "Pay Per Use Multimedia Messaging"
            },
            {
              "Action": "ADD",
              "BillingCode": "WXP1O",
              "Characteristics": {
                "AddOnSolutionCharacterstics": {},
                "CommonCharacteristics": {},
                "InternetLineItemChars": {},
                "VOIPLineItemChars": {},
                "WirelessLineItemChars": {
                  "ADTM": {},
                  "OfferType": "P",
                  "PDP": {},
                  "TradeInInfo": {}
                }
              },
              "DisplayName": "[discontinued] Data Pay Per Use",
              "GroupRefs": {
                "GroupRef": [
                  "GROUP_01"
                ]
              },
              "Id": "losg136762526216002_sku22530391",
              "LineItemSequence": 23,
              "Payments": {},
              "Price": {
                "Amount": 0,
                "CurrencyType": "USD",
                "PriceType": "RC",
                "TaxInfo": {
                  "Amount": 0
                },
                "Total": 0
              },
              "ProductCode": "WIRELESS_10",
              "ProductSku": "NOT_AVAILABLE",
              "ProductType": "INCLUDED_FEATURE",
              "Quantity": 1,
              "SupplyChainInfo": {},
              "SystemName": "MEDIA NET PAY PER USE"
            },
            {
              "Action": "ADD",
              "BillingCode": "DBNC",
              "Characteristics": {
                "AddOnSolutionCharacterstics": {},
                "CommonCharacteristics": {},
                "InternetLineItemChars": {},
                "VOIPLineItemChars": {},
                "WirelessLineItemChars": {
                  "ADTM": {},
                  "OfferType": "P",
                  "PDP": {},
                  "TradeInInfo": {}
                }
              },
              "DisplayName": "Detailed Billing - Nation",
              "GroupRefs": {
                "GroupRef": [
                  "GROUP_01"
                ]
              },
              "Id": "losg136762526216002_sku19010987",
              "LineItemSequence": 24,
              "Payments": {},
              "Price": {
                "Amount": 0,
                "CurrencyType": "USD",
                "PriceType": "RC",
                "TaxInfo": {
                  "Amount": 0
                },
                "Total": 0
              },
              "ProductCode": "WIRELESS_11",
              "ProductSku": "NOT_AVAILABLE",
              "ProductType": "INCLUDED_FEATURE",
              "Quantity": 1,
              "SupplyChainInfo": {},
              "SystemName": "Detailed Billing - Nation"
            },
            {
              "Action": "ADD",
              "BillingCode": "GOVP300U",
              "Characteristics": {
                "AddOnSolutionCharacterstics": {},
                "CommonCharacteristics": {},
                "InternetLineItemChars": {},
                "VOIPLineItemChars": {},
                "WirelessLineItemChars": {
                  "ADTM": {},
                  "OfferType": "P",
                  "PDP": {},
                  "TradeInInfo": {}
                }
              },
              "DisplayName": "Government Nation Pooled 300 (UNW/UM2M)",
              "GroupRefs": {
                "GroupRef": [
                  "GROUP_01"
                ]
              },
              "Id": "alcitem24184615666364",
              "LineItemSequence": 12,
              "Payments": {
                "Payment": [
                  {
                    "Amount": 0,
                    "CurrencyType": "USD",
                    "NoOfInstallment": 0,
                    "PaymentOptionRef": "PAYMENT_OPTION_02"
                  }
                ]
              },
              "Price": {
                "Amount": 104,
                "CurrencyType": "USD",
                "InstallmentEligibility": "N",
                "MSRP": 104,
                "PriceType": "RC",
                "TaxInfo": {
                  "Amount": 0
                },
                "Total": 48.75
              },
              "ProductCode": "WIRELESS_8",
              "ProductSku": "NOT_AVAILABLE",
              "ProductType": "PLAN",
              "PromotionRefs": {
                "PromotionRef": [
                  "PROMOTION_02",
                  "PROMOTION_03",
                  "PROMOTION_04"
                ]
              },
              "Quantity": 1,
              "SupplyChainInfo": {},
              "SystemName": "GOVTNBPNTN300UMUNW"
            },
            {
              "Action": "ADD",
              "BillingCode": "RGOVEJB5",
              "Characteristics": {
                "AddOnSolutionCharacterstics": {},
                "CommonCharacteristics": {},
                "InternetLineItemChars": {},
                "VOIPLineItemChars": {},
                "WirelessLineItemChars": {
                  "ADTM": {},
                  "OfferType": "P",
                  "PDP": {},
                  "TradeInInfo": {}
                }
              },
              "DisplayName": "ODN Enterprise Data Plan for iPhone on 4G LTE with\n\t\t\t\t\tUnlimited Text Messaging-R (RGOVEJB5)",
              "GroupRefs": {
                "GroupRef": [
                  "GROUP_01"
                ]
              },
              "Id": "alcitem24184616280609",
              "LineItemSequence": 16,
              "Payments": {
                "Payment": [
                  {
                    "Amount": 0,
                    "CurrencyType": "USD",
                    "NoOfInstallment": 0,
                    "PaymentOptionRef": "PAYMENT_OPTION_02"
                  }
                ]
              },
              "Price": {
                "Amount": 65,
                "CurrencyType": "USD",
                "InstallmentEligibility": "N",
                "MSRP": 65,
                "PriceType": "RC",
                "TaxInfo": {
                  "Amount": 0
                },
                "Total": 26.25
              },
              "ProductCode": "WIRELESS_12",
              "ProductSku": "NOT_AVAILABLE",
              "ProductType": "OPTIONAL_FEATURE",
              "PromotionRefs": {
                "PromotionRef": [
                  "PROMOTION_05",
                  "PROMOTION_04"
                ]
              },
              "Quantity": 1,
              "SupplyChainInfo": {},
              "SystemName": "DATA MSG UN LTE IP E"
            },
            {
              "Action": "ADD",
              "BillingCode": "NOT_AVAILABLE",
              "Characteristics": {
                "AddOnSolutionCharacterstics": {},
                "CommonCharacteristics": {},
                "InternetLineItemChars": {},
                "VOIPLineItemChars": {},
                "WirelessLineItemChars": {
                  "ADTM": {},
                  "PDP": {},
                  "TradeInInfo": {}
                }
              },
              "Description": "ACTIVATION_FEE",
              "DisplayName": "ActivationFee",
              "GroupRefs": {
                "GroupRef": [
                  "GROUP_01"
                ]
              },
              "Id": "alcitem24184615767745",
              "LineItemSequence": 17,
              "LocationID": "K008",
              "Payments": {
                "Payment": [
                  {
                    "Amount": 0,
                    "CurrencyType": "USD",
                    "PaymentOptionRef": "PAYMENT_OPTION_01"
                  }
                ]
              },
              "Price": {
                "Amount": 0,
                "CurrencyType": "USD",
                "InstallmentEligibility": "N",
                "MSRP": 45,
                "PriceType": "NRC",
                "TaxInfo": {
                  "Amount": 0
                },
                "Total": 0
              },
              "ProductCode": "WIRELESS_13",
              "ProductSku": "NOT_AVAILABLE",
              "ProductType": "MISC_CHARGE",
              "PromotionRefs": {
                "PromotionRef": [
                  "PROMOTION_06"
                ]
              },
              "Quantity": 1,
              "SupplyChainInfo": {},
              "SystemName": "ACTIVATION_FEE"
            },
            {
              "BillingCode": "NOT_AVAILABLE",
              "Characteristics": {
                "AddOnSolutionCharacterstics": {},
                "CommonCharacteristics": {},
                "InternetLineItemChars": {},
                "VOIPLineItemChars": {},
                "WirelessLineItemChars": {
                  "ADTM": {},
                  "PDP": {},
                  "TradeInInfo": {}
                }
              },
              "DisplayName": "AUTO_PAYMENT",
              "GroupRefs": {
                "GroupRef": [
                  "GROUP_01"
                ]
              },
              "Id": "LINEITEM_01",
              "LineItemSequence": 0,
              "Payments": {
                "Payment": [
                  {
                    "Amount": 0,
                    "CurrencyType": "USD",
                    "NoOfInstallment": 0,
                    "PaymentOptionRef": "PAYMENT_OPTION_02"
                  }
                ]
              },
              "Price": {
                "Amount": 104,
                "CurrencyType": "USD",
                "InstallmentEligibility": "N",
                "MSRP": 104,
                "PriceType": "RC",
                "TaxInfo": {
                  "Amount": 0
                },
                "Total": 48.75
              },
              "ProductCode": "NOT_AVAILABLE",
              "ProductType": "MISC_CHARGE",
              "Quantity": 1,
              "SupplyChainInfo": {},
              "SystemName": "AUTO_PAYMENT"
            }
          ]
        },
        "LoginProfile": {
          "OrderInitiator": "TCM",
          "ProfileId": "al44721900941",
          "UserId": "JRaygoza"
        },
        "ManageCallList": {},
        "Names": {
          "Name": [
            {
              "FirstName": "JOHN",
              "Id": "NAME_01",
              "LastName": "RAYGOZA",
              "PrimaryContactPhone": [
                {
                  "ConsentDetails": {},
                  "ContactPhoneType": "HOME_PHONE",
                  "PhoneNumber": "9167340010"
                }
              ]
            },
            {
              "FirstName": "AMY",
              "Id": "NAME_02",
              "LastName": "YEE",
              "PrimaryContactPhone": [
                {
                  "ConsentDetails": {},
                  "ContactPhoneType": "HOME_PHONE",
                  "PhoneNumber": "9167348000"
                }
              ]
            },
            {
              "FirstName": "JOHN",
              "Id": "NAME_03",
              "LastName": "RAYGOZA",
              "PrimaryContactPhone": [
                {
                  "ConsentDetails": {},
                  "ContactPhoneType": "HOME_PHONE",
                  "PhoneNumber": "9167340010"
                }
              ]
            },
            {
              "FirstName": "ANDREW",
              "Id": "NAME_04",
              "LastName": "RAMIREZ",
              "PrimaryContactPhone": [
                {
                  "ConsentDetails": {},
                  "ContactPhoneType": "HOME_PHONE",
                  "PhoneNumber": "9167340010"
                }
              ]
            }
          ]
        },
        "OCEOrderNumber": "D57470002",
        "OrderContact": {
          "NameRef": "NAME_01"
        },
        "OrderSource": {
          "AdditionalDetails": {
            "AdditionalDetail": [
              {
                "Code": "PremierSubChannel",
                "Type": "Order",
                "Value": "web-PremierWebCruDesktop"
              },
              {
                "Code": "BUYFLOW",
                "Type": "Order",
                "Value": "NON-NEWCO"
              },
              {
                "Code": "SENDER",
                "Type": "Order",
                "Value": "Premier"
              }
            ]
          },
          "Application": "PREMIER",
          "BrowserID": "A0014987413667289bbd7d59-a4b4-40da-adaa-50781101b40c\n\t\t\t",
          "Channel": "CRU-MOBILITY",
          "City": "Sacramento",
          "ClientIP": "152.79.255.200",
          "ClientType": "DESKTOP",
          "Locale": "en_US",
          "Region": "US",
          "Zip": "95817"
        },
        "OrderStatus": {
          "Status": "IN_PROGRESS",
          "SubStatus": "IN_QUEUE"
        },
        "OrderType": "CREATE",
        "ParentOrderNumber": null,
        "PaymentOptions": {
          "PaymentOption": [
            {
              "CAPMConfig": {},
              "Id": "PAYMENT_OPTION_01",
              "PaymentMethod": {
                "BTM": {
                  "EquipmentType": "G",
                  "SubscriberNumber": "9999999999",
                  "TotalAmount": 162.99
                }
              },
              "PaymentSequence": 1
            },
            {
              "CAPMConfig": {},
              "Id": "PAYMENT_OPTION_02",
              "PaymentMethod": {
                "BTM": {
                  "EquipmentType": "G",
                  "SubscriberNumber": "9999999999",
                  "TotalAmount": 0
                }
              },
              "PaymentSequence": 2
            }
          ]
        },
        "PremierGroupId": "2000900019",
        "PremierGroupName": "UC Davis Medical",
        "Promotions": {
          "Promotion": [
            {
              "DisplayLevel": "ITEM",
              "DisplaySequence": 1,
              "FixedAmount": 0,
              "Id": "PROMOTION_06",
              "PromotionCode": "promo11149200024",
              "PromotionCycle": "ONETIME",
              "PromotionId": "promo11149200024",
              "PromotionName": "Waived Activation Fee",
              "PromotionType": "PROMOTION",
              "UnitOfMeasurement": "FLATOFF"
            },
            {
              "DisplayLevel": "ITEM",
              "DisplaySequence": 3,
              "FixedAmount": 4,
              "Id": "PROMOTION_03",
              "PromotionCode": "promo11259000042",
              "PromotionCycle": "MONTHLY",
              "PromotionId": "promo11259000042",
              "PromotionName": "$4 off Government Nation Pooled 300/300U Voice Plan\n\t\t\t\t\twith Select $65/$80 Enterprise Data Plans with Unlimited Messaging\n\t\t\t\t\t(includes DataPro)",
              "PromotionType": "PROMOTION",
              "UnitOfMeasurement": "FLATOFF"
            },
            {
              "DisplayLevel": "ITEM",
              "DisplaySequence": 5,
              "Id": "PROMOTION_04",
              "Percent": 25,
              "PromotionCode": "promo6861000021",
              "PromotionCycle": "MONTHLY",
              "PromotionId": "promo6861000021",
              "PromotionName": "25% Service Discount",
              "PromotionType": "PROMOTION",
              "UnitOfMeasurement": "PERCENTAGE"
            },
            {
              "DisplayLevel": "ITEM",
              "DisplaySequence": 5,
              "Id": "PROMOTION_01",
              "Percent": 30,
              "PromotionCode": "promo11011400043",
              "PromotionCycle": "ONETIME",
              "PromotionId": "promo11011400043",
              "PromotionName": "30% Accessory Discount",
              "PromotionType": "PROMOTION",
              "UnitOfMeasurement": "PERCENTAGE"
            },
            {
              "DisplayLevel": "ITEM",
              "DisplaySequence": 3,
              "FixedAmount": 30,
              "Id": "PROMOTION_05",
              "PromotionCode": "promo11263100049",
              "PromotionCycle": "MONTHLY",
              "PromotionId": "promo11263100049",
              "PromotionName": "$30 off Select $65 BlackBerry/Smartphone/iPhone\n\t\t\t\t\tEnterprise with Unlimited Messaging Add On Plans with Government\n\t\t\t\t\tNation Pooled 300/300U/400/400U/600/1000 or $15.99 Government\n\t\t\t\t\tNation Pooled Plan (excludes DataPro)",
              "PromotionType": "PROMOTION",
              "UnitOfMeasurement": "FLATOFF"
            },
            {
              "DisplayLevel": "ITEM",
              "DisplaySequence": 3,
              "FixedAmount": 5,
              "Id": "PROMOTION_02",
              "PromotionCode": "promo11185800052",
              "PromotionCycle": "MONTHLY",
              "PromotionId": "promo11185800052",
              "PromotionName": "$5 off GOV Nation Pooled 300/300U/400/400U/600/1000\n\t\t\t\t\tVoice Plan",
              "PromotionType": "PROMOTION",
              "UnitOfMeasurement": "FLATOFF"
            }
          ]
        },
        "RequestId": "PREMIER:1503956204811",
        "RequestType": "SOR",
        "SalesChannel": "B",
        "SalesCode": "6F728",
        "ShippingInfos": {
          "ShippingInfo": [
            {
              "AddressRef": "ADDRESS_02",
              "Id": "SHIPPING_INFO_01",
              "NameRef": "NAME_03",
              "ShippingCode": "U2",
              "ShippingInfoSequence": 1,
              "ShippingMethod": "UPSGround",
              "ShippingPriceCode": "88888"
            }
          ]
        },
        "SubmitedDate": 1503959688000,
        "TCs": {
          "TCAccepted": [
            {
              "Accepted": "Y",
              "AgreementType": "WCA",
              "Id": "TC_01",
              "IsOrderLevel": true,
              "Timestamp": 1503959688000,
              "Version": "DEFAULT_VERSION"
            }
          ]
        },
        "TotalPrice": {},
        "UpdatedDate": 1504064567000,
        "Version": 2
      }
    }
  ]
}
```




