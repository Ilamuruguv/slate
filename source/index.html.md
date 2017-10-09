---
title: API Reference

language_tabs: # must be one of https://git.io/vQNgJ
  - java 
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
Header(s)
		Use the Bitmap and the Auth token generated with the user id and password using base64 encoding. 
		
		X-APP-Bitmap 0000000000001000000000000000000000000000000000100000000000000010	
		Authorization Basic U0hBUkVEU0VSVklDRVM6U1RBUlRIUjMzUk9DS1M=

```java

			String userName = "USER";
			String password = "AUTH";
			String userpass = userName + ":" + password;
			String 	basicAuth = "Basic " + new String(new Base64().encode(userpass.getBytes()));
```
	
			

# ProcessOrder API - V6 
		OCE process order API accepts the JSON payload  which complaints to the API specifications and returns the JSON acknowledgement response.  Please refer the [order](#order) json strucuture explained in below.
	


### HTTP(S) Request
`POST http(s)://host:port/restservices/oce/v6/orders`



![postman](/images/postman.png) Get the [Postman collection for NEW DTV standalone] (https://www.getpostman.com/collections/7cecd0d9e68134fe0b61) from this link to test with the OCE test instance.

> To test the process order api in java dme2 client, use the below code:


```java
	try { 
			
			System.setProperty("AFT_DME2_HTTP_EXCHANGE_TRACE_ON", "true"); 
			
			System.setProperty("AFT_LATITUDE", "34.087063"); 
			System.setProperty("AFT_LONGITUDE", "-84.275422");
			
			System.setProperty("AFT_ENVIRONMENT", "AFTUAT"); 
			System.setProperty("AFT_DME2_CONN_IDLE_TIMEOUTMS", "3000"); 
			System.setProperty("DME2.DEBUG", "false");
			
			//FOR HTTPS Non Prod
			System.setProperty("AFT_DME2_CLIENT_IGNORE_SSL_CONFIG", "false");
			System.setProperty("AFT_DME2_CLIENT_SSL_INCLUDE_PROTOCOLS", "TLSv1.2,TLSv1.1,TLSv1,TLS1.0, TLS2.0");
			
			
			System.setProperty("AFT_DME2_CLIENT_KEYSTORE_PASSWORD", " ");
			
			String userName = "USER";
			String password = "AUTH";
			String userpass = userName + ":" + password;
			String 	basicAuth = "Basic " + new String(new Base64().encode(userpass.getBytes()));
			
			System.out.println(basicAuth);
			
			HashMap<String, String> headerMap = new HashMap<String, String>(); 
			headerMap.put("Accept", "application/json"); 
			headerMap.put("Content-type", "application/json");
			headerMap.put("Authorization", basicAuth);
			headerMap.put("X-APP-Bitmap", "0000000000000001000000000000000000000000000001010000000000000000");
			// Note: envConetxt will determine the Test and Dev. AFT_LATITUDE and AFT_LONGITUDE will be looked and near by location will be taken
			//Current Dev Env
		
			
			
			String service = "http://URL/restservices/oce/v5?version=6&envContext=TEST&routeOffer=DEFAULT";
			
			
			String context = "/orders";
			String jsonRequestFile = "REQEST JSON";
			
			DME2Client sender = new DME2Client(new URI(service), 30000); 
			FileReader fileReader = new FileReader(new File(jsonRequestFile));
			JSONParser parser = new JSONParser();
			Object obj = parser.parse(fileReader); 
			JSONObject json =  (JSONObject) obj;
			
			sender.setAllowAllHttpReturnCodes(true);// Don't break on code!=200 
			sender.setMethod("POST"); 
			sender.setHeaders(headerMap); 
			sender.setPayload(json.toString());
			
			// This is required to determine which the REST service for the particular application
			sender.setSubContext(context); 
			
			DME2RestfulHandler replyHandler = new DME2RestfulHandler(service); 
			sender.setReplyHandler(replyHandler); 
			sender.send(); 
			
			ResponseInfo reply = replyHandler.getResponseInfo(120000); 
			
			

		} catch (DME2Exception de) { 
			de.printStackTrace(); 
		} catch (Exception e) { 
			e.printStackTrace(); 
		}
```

```shell
# With shell, you can just pass the correct header with each request
curl "api_endpoint_here"
  -H "Authorization: Basic U0hBUkVEU0VSVklDRVM6U1RBUlRIUjMzUk9DS1M="
  -H "X-APP-Bitmap: 0000000000001000000000000000000000000000000000100000000000000010"
  -
```

```javascript

		
		function jscalltoOCE () {	
			ajax http call imeplelemtation
		} 
```




> Request BODY JSON structured like this:



```json

{
  "customerOrderNumber" : "20-301100009625088",
  "orderType" : "CREATE",
  "createdDate" : 1503370818288,
  "submittedDate" : 1503371365453,
  "productGroups" : {
    "group" : [ {
      "id" : "GROUP_01",
      "name" : "Package",
      "type" : "PACKAGE",
      "sequence" : 1,
      "characteristics" : {
        "packageCharacteristics" : {
          "category" : "OFFER",
          "code" : "422383389",
          "type" : "NEW"
        }
      }
    }, {
      "id" : "GROUP_02",
      "name" : "XTRA All Included",
      "type" : "LINE_OF_SERVICE",
      "sequence" : 2,
      "characteristics" : {
        "losgCharacteristics" : {
          "losgReferenceId" : "dtv",
          "sequence" : 1,
          "losgType" : "NEW",
          "productCategory" : "DIRECTV",
          "dealerCode" : "Z0066",
          "accountReference" : "ACCOUNT_01",
          "serviceLocationReference" : "ADDRESS_01",
          "serviceQualificationReference" : "SERVICE_QLFY_01",
          "termsAndConditionReferences" : {
            "termsAndConditionReference" : [ "TC_02" ]
          },
          "schedulingDetailReference" : "SCHEDULINGINFO_01",
          "direcTVLOSCharacteristics" : {
            "offerLanguage" : "English",
            "dealerId" : "1782681",
            "marketingSourceCode" : "7111",
            "moveInOrder" : "N"
          },
          "fulfillmentMethod" : "DF",
          "additionalDetails" : {
            "additionalDetail" : [ {
              "type" : "OMRR",
              "code" : "parentComponentCode",
              "value" : "ATTDVMAIN"
            } ]
          }
        }
      }
    } ]
  },
  "lineItems" : {
    "lineItem" : [ {
      "id" : "99465092577",
      "productCode" : "P103354",
      "productSKU" : "sku7650336",
      "billingCode" : "88849634",
      "productType" : "PLAN",
      "displayName" : "XTRA All Included",
      "systemName" : "DTV:XTRA all included",
      "action" : "ADD",
      "price" : {
        "amount" : 70.00,
        "currencyType" : "USD",
        "msrp" : 124.00,
        "priceType" : "RC",
        "total" : 70.00
      },
      "quantity" : 1,
      "promotionReferences" : {
        "promotionReference" : [ "PROMOTION_01" ]
      },
      "groupReferences" : {
        "groupReference" : [ "GROUP_02", "GROUP_01" ]
      },
      "characteristics" : {
        "commonCharacteristics" : {
          "componentConfigurations" : [ {
            "componentCode" : "ATTDTV",
            "componentOperations" : [ {
              "operationNames" : [ "MOORequest" ]
            }, {
              "operationNames" : [ "PUSPO1Request" ]
            } ],
            "componentPath" : "ATTDTV",
            "componentMapRequiredIndicator" : true,
            "attributes" : [ {
              "attributeCode" : "BasePkg",
              "attributeValue" : "XTRAAll",
              "attributeOperations" : [ {
                "operationNames" : [ "MOORequest" ]
              }, {
                "operationNames" : [ "PUSPO1Request" ]
              } ]
            } ]
          }, {
            "componentCode" : "ATTDV",
            "componentOperations" : [ {
              "operationNames" : [ "IWFARequest" ]
            } ],
            "componentPath" : "ATTDV",
            "componentMapRequiredIndicator" : true
          }, {
            "componentCode" : "DTV",
            "componentOperations" : [ {
              "operationNames" : [ "IWFARequest" ]
            } ],
            "componentPath" : "DTV",
            "componentMapRequiredIndicator" : true
          }, {
            "componentCode" : "programming",
            "componentOperations" : [ {
              "operationNames" : [ "QPRequest" ]
            }, {
              "operationNames" : [ "RQRequest" ]
            } ],
            "componentPath" : "programming",
            "componentMapRequiredIndicator" : true,
            "attributes" : [ {
              "attributeKey" : "DWSNew.ProgrammingCoreNew.ProgrammingCoreNew.Languages.AIBasePackages.AllInclusive.BasePackages.BasePackages",
              "attributeCode" : "optionKey",
              "attributeValue" : "P103354",
              "attributeOperations" : [ {
                "operationNames" : [ "QPRequest" ]
              }, {
                "operationNames" : [ "RQRequest" ]
              } ]
            } ]
          } ],
          "ignorePricePlanCode" : "N"
        }
      }
    }, {
      "id" : "99465092995",
      "productCode" : "H00000038927",
      "productSKU" : "sku7650361",
      "billingCode" : "2",
      "productType" : "HARDGOOD",
      "displayName" : "Genie HD DVR",
      "systemName" : "IncludedGenieHDDVR",
      "action" : "ADD",
      "price" : {
        "amount" : 0.00,
        "currencyType" : "USD",
        "msrp" : 0.00,
        "priceType" : "RC",
        "total" : 0.00
      },
      "quantity" : 1,
      "groupReferences" : {
        "groupReference" : [ "GROUP_02", "GROUP_01" ]
      },
      "characteristics" : {
        "commonCharacteristics" : {
          "componentConfigurations" : [ {
            "componentCode" : "DTVGenie",
            "componentOperations" : [ {
              "operationNames" : [ "MOORequest" ]
            }, {
              "operationNames" : [ "PUSPO1Request" ]
            } ],
            "componentPath" : "ATTDTVCPE|DTVGenie",
            "componentMapRequiredIndicator" : true
          }, {
            "componentCode" : "ATTDTVCPE",
            "componentOperations" : [ {
              "operationNames" : [ "MOORequest" ]
            }, {
              "operationNames" : [ "PUSPO1Request" ]
            } ],
            "componentPath" : "ATTDTVCPE",
            "componentMapRequiredIndicator" : true,
            "attributes" : [ {
              "attributeCode" : "DTVGenie",
              "attributeValue" : "@QUANTITY@",
              "attributeOperations" : [ {
                "operationNames" : [ "MOORequest" ]
              }, {
                "operationNames" : [ "PUSPO1Request" ]
              } ]
            }, {
              "attributeCode" : "numberOfTvs",
              "attributeValue" : "@QUANTITY@",
              "attributeOperations" : [ {
                "operationNames" : [ "MOORequest" ]
              }, {
                "operationNames" : [ "PUSPO1Request" ]
              } ]
            } ]
          }, {
            "componentCode" : "DTSTB",
            "componentOperations" : [ {
              "operationNames" : [ "IWFARequest" ]
            } ],
            "componentPath" : "DTCP|DTSTB",
            "componentMapRequiredIndicator" : true
          }, {
            "componentCode" : "DTVCPE",
            "componentOperations" : [ {
              "operationNames" : [ "FVPD1Request" ]
            } ],
            "componentPath" : "DTVCPE",
            "componentMapRequiredIndicator" : true,
            "attributes" : [ {
              "attributeCode" : "materialCode",
              "attributeValue" : "100003360",
              "attributeOperations" : [ {
                "operationNames" : [ "FVPD1Request" ]
              } ]
            }, {
              "attributeCode" : "SKUCode",
              "attributeValue" : "H00000038927",
              "attributeOperations" : [ {
                "operationNames" : [ "FVPD1Request" ]
              } ]
            } ]
          }, {
            "componentCode" : "equipment",
            "componentOperations" : [ {
              "operationNames" : [ "QPRequest" ]
            }, {
              "operationNames" : [ "RQRequest" ]
            } ],
            "componentPath" : "equipment",
            "componentMapRequiredIndicator" : true,
            "attributes" : [ {
              "attributeKey" : "DWSNew.Hardware.Hardware.ReceiverTotalOrderCheck.ReceiverTotalOrderCount.OnHowManyReceivers",
              "attributeCode" : "quantity",
              "attributeValue" : "@#_TVCount@",
              "attributeOperations" : [ {
                "operationNames" : [ "QPRequest" ]
              }, {
                "operationNames" : [ "RQRequest" ]
              } ]
            }, {
              "attributeKey" : "DWSNew.Hardware.Hardware.ReceiverLeased.ReceiverLeased.ReceiverLeased",
              "attributeCode" : "quantity",
              "attributeValue" : "@#_H00000038927@",
              "attributeOperations" : [ {
                "operationNames" : [ "QPRequest" ]
              }, {
                "operationNames" : [ "RQRequest" ]
              } ]
            } ]
          }, {
            "componentCode" : "DTVCP",
            "componentOperations" : [ {
              "operationNames" : [ "IWFARequest" ]
            } ],
            "componentPath" : "DTV|DTVCP",
            "componentMapRequiredIndicator" : true,
            "attributes" : [ {
              "attributeCode" : "installationType",
              "attributeValue" : "Tech",
              "attributeOperations" : [ {
                "operationNames" : [ "IWFARequest" ]
              } ]
            } ]
          } ],
          "ignorePricePlanCode" : "N"
        }
      },
      "hardGood" : {
        "hardGoodType" : "DVR"
      }
    }, {
      "id" : "99465092996",
      "productCode" : "H00000000745",
      "productSKU" : "sku7650365",
      "billingCode" : "2",
      "productType" : "HARDGOOD",
      "displayName" : "Wireless Genie Mini",
      "systemName" : "IncludedWirelessGenieMini",
      "action" : "ADD",
      "price" : {
        "amount" : 0.00,
        "currencyType" : "USD",
        "msrp" : 0.00,
        "priceType" : "RC",
        "total" : 0.00
      },
      "quantity" : 1,
      "groupReferences" : {
        "groupReference" : [ "GROUP_02", "GROUP_01" ]
      },
      "characteristics" : {
        "commonCharacteristics" : {
          "componentConfigurations" : [ {
            "componentCode" : "DTVWirelessGenie",
            "componentOperations" : [ {
              "operationNames" : [ "MOORequest" ]
            }, {
              "operationNames" : [ "PUSPO1Request" ]
            } ],
            "componentPath" : "ATTDTVCPE|DTVWirelessGenie",
            "componentMapRequiredIndicator" : true
          }, {
            "componentCode" : "ATTDTVCPE",
            "componentOperations" : [ {
              "operationNames" : [ "MOORequest" ]
            }, {
              "operationNames" : [ "PUSPO1Request" ]
            } ],
            "componentPath" : "ATTDTVCPE",
            "componentMapRequiredIndicator" : true,
            "attributes" : [ {
              "attributeCode" : "DTVWGenieMini",
              "attributeValue" : "@QUANTITY@",
              "attributeOperations" : [ {
                "operationNames" : [ "MOORequest" ]
              }, {
                "operationNames" : [ "PUSPO1Request" ]
              } ]
            }, {
              "attributeCode" : "numberOfTvs",
              "attributeValue" : "@QUANTITY@",
              "attributeOperations" : [ {
                "operationNames" : [ "MOORequest" ]
              }, {
                "operationNames" : [ "PUSPO1Request" ]
              } ]
            } ]
          }, {
            "componentCode" : "DTSTB",
            "componentOperations" : [ {
              "operationNames" : [ "IWFARequest" ]
            } ],
            "componentPath" : "DTCP|DTSTB",
            "componentMapRequiredIndicator" : true
          }, {
            "componentCode" : "DTVCPE",
            "componentOperations" : [ {
              "operationNames" : [ "FVPD1Request" ]
            } ],
            "componentPath" : "DTVCPE",
            "componentMapRequiredIndicator" : true,
            "attributes" : [ {
              "attributeCode" : "materialCode",
              "attributeValue" : "100003357",
              "attributeOperations" : [ {
                "operationNames" : [ "FVPD1Request" ]
              } ]
            }, {
              "attributeCode" : "SKUCode",
              "attributeValue" : "H00000000745",
              "attributeOperations" : [ {
                "operationNames" : [ "FVPD1Request" ]
              } ]
            } ]
          }, {
            "componentCode" : "equipment",
            "componentOperations" : [ {
              "operationNames" : [ "QPRequest" ]
            }, {
              "operationNames" : [ "RQRequest" ]
            } ],
            "componentPath" : "equipment",
            "componentMapRequiredIndicator" : true,
            "attributes" : [ {
              "attributeKey" : "DWSNew.Hardware.Hardware.ReceiverTotalOrderCheck.ReceiverTotalOrderCount.OnHowManyReceivers",
              "attributeCode" : "quantity",
              "attributeValue" : "@#_TVCount@",
              "attributeOperations" : [ {
                "operationNames" : [ "QPRequest" ]
              }, {
                "operationNames" : [ "RQRequest" ]
              } ]
            }, {
              "attributeKey" : "DWSNew.Hardware.Hardware.HomeMediaCenterClient.HomeMediaCenterClient.HomeMediaCenterClient.HomeMediaCenterClientLeased",
              "attributeCode" : "quantity",
              "attributeValue" : "@#_H00000000745@",
              "attributeOperations" : [ {
                "operationNames" : [ "QPRequest" ]
              }, {
                "operationNames" : [ "RQRequest" ]
              } ]
            } ]
          }, {
            "componentCode" : "DTVCP",
            "componentOperations" : [ {
              "operationNames" : [ "IWFARequest" ]
            } ],
            "componentPath" : "DTV|DTVCP",
            "componentMapRequiredIndicator" : true,
            "attributes" : [ {
              "attributeCode" : "installationType",
              "attributeValue" : "Tech",
              "attributeOperations" : [ {
                "operationNames" : [ "IWFARequest" ]
              } ]
            } ]
          } ],
          "ignorePricePlanCode" : "N"
        }
      },
      "hardGood" : {
        "hardGoodType" : "STB"
      }
    }, {
      "id" : "99465092997",
      "productCode" : "P6376",
      "productSKU" : "sku7650429",
      "billingCode" : "111",
      "productType" : "OPTIONAL_FEATURE",
      "displayName" : "Advanced Receiver Fee ",
      "systemName" : "DTV Included Advanced Receiver Fee",
      "action" : "ADD",
      "price" : {
        "amount" : 0.00,
        "currencyType" : "USD",
        "msrp" : 0.00,
        "priceType" : "RC",
        "total" : 0.00
      },
      "quantity" : 1,
      "groupReferences" : {
        "groupReference" : [ "GROUP_02", "GROUP_01" ]
      },
      "characteristics" : { }
    }, {
      "id" : "99465092998",
      "productCode" : "H00000038927",
      "productSKU" : "sku7680379",
      "billingCode" : "88855444",
      "productType" : "HARDGOOD",
      "displayName" : "Genie HD DVR",
      "systemName" : "DTV:NRCDueToday:Included Genie HD DVR",
      "action" : "ADD",
      "price" : {
        "amount" : 0.00,
        "currencyType" : "USD",
        "msrp" : 299.00,
        "priceType" : "NRC",
        "total" : 0.00
      },
      "quantity" : 1,
      "promotionReferences" : {
        "promotionReference" : [ "PROMOTION_02" ]
      },
      "groupReferences" : {
        "groupReference" : [ "GROUP_02", "GROUP_01" ]
      },
      "characteristics" : {
        "commonCharacteristics" : {
          "componentConfigurations" : [ {
            "componentCode" : "DTSTB",
            "componentOperations" : [ {
              "operationNames" : [ "IWFARequest" ]
            } ],
            "componentPath" : "DTCP|DTSTB",
            "componentMapRequiredIndicator" : true
          }, {
            "componentCode" : "lineItemIdentifier",
            "componentOperations" : [ {
              "operationNames" : [ "CalculateTaxRequest" ]
            } ],
            "componentPath" : "lineItemIdentifier",
            "componentMapRequiredIndicator" : true,
            "attributes" : [ {
              "attributeCode" : "omsProductId",
              "attributeValue" : "38927",
              "attributeOperations" : [ {
                "operationNames" : [ "CalculateTaxRequest" ]
              } ]
            } ]
          } ],
          "ignorePricePlanCode" : "N"
        }
      },
      "hardGood" : {
        "hardGoodType" : "DVR"
      }
    }, {
      "id" : "99465092999",
      "productCode" : "H00000000745",
      "productSKU" : "sku7680390",
      "billingCode" : "88855464",
      "productType" : "HARDGOOD",
      "displayName" : "Wireless Genie Mini",
      "systemName" : "DTV:NRCDueToday:Included Wireless Genie Mini",
      "action" : "ADD",
      "price" : {
        "amount" : 0.00,
        "currencyType" : "USD",
        "msrp" : 99.00,
        "priceType" : "NRC",
        "total" : 0.00
      },
      "quantity" : 1,
      "promotionReferences" : {
        "promotionReference" : [ "PROMOTION_03" ]
      },
      "groupReferences" : {
        "groupReference" : [ "GROUP_02", "GROUP_01" ]
      },
      "characteristics" : {
        "commonCharacteristics" : {
          "componentConfigurations" : [ {
            "componentCode" : "DTSTB",
            "componentOperations" : [ {
              "operationNames" : [ "IWFARequest" ]
            } ],
            "componentPath" : "DTCP|DTSTB",
            "componentMapRequiredIndicator" : true
          }, {
            "componentCode" : "lineItemIdentifier",
            "componentOperations" : [ {
              "operationNames" : [ "CalculateTaxRequest" ]
            } ],
            "componentPath" : "lineItemIdentifier",
            "componentMapRequiredIndicator" : true,
            "attributes" : [ {
              "attributeCode" : "omsProductId",
              "attributeValue" : "745",
              "attributeOperations" : [ {
                "operationNames" : [ "CalculateTaxRequest" ]
              } ]
            } ]
          } ],
          "ignorePricePlanCode" : "N"
        }
      },
      "hardGood" : {
        "hardGoodType" : "STB"
      }
    }, {
      "id" : "99465093000",
      "productCode" : "B103322",
      "productSKU" : "sku7650501",
      "billingCode" : "88835094",
      "productType" : "OPTIONAL_FEATURE",
      "displayName" : "DIRECTV wireless receiver upgrade fee",
      "systemName" : "DIRECTV wireless receiver upgrade fee",
      "action" : "ADD",
      "price" : {
        "amount" : 99.00,
        "currencyType" : "USD",
        "msrp" : 99.00,
        "priceType" : "NRC",
        "total" : 99.00
      },
      "quantity" : 1,
      "groupReferences" : {
        "groupReference" : [ "GROUP_02", "GROUP_01" ]
      },
      "characteristics" : {
        "commonCharacteristics" : {
          "componentConfigurations" : [ {
            "componentCode" : "WirelessBrdg",
            "componentOperations" : [ {
              "operationNames" : [ "MOORequest" ]
            }, {
              "operationNames" : [ "PUSPO1Request" ]
            } ],
            "componentPath" : "AccDV|WirelessBrdg",
            "componentMapRequiredIndicator" : true
          } ],
          "ignorePricePlanCode" : "N"
        }
      }
    }, {
      "id" : "LINEITEM_08",
      "productCode" : "NOT_AVAILABLE",
      "billingCode" : "NOT_AVAILABLE",
      "productType" : "OPTIONAL_FEATURE",
      "displayName" : "Paperless_Bill",
      "systemName" : "PAPERLESS_BILL",
      "price" : {
        "amount" : 0,
        "currencyType" : "USD",
        "msrp" : 0,
        "priceType" : "RC",
        "total" : 0
      },
      "groupReferences" : {
        "groupReference" : [ "GROUP_02" ]
      }
    } ]
  },
  "names" : {
    "name" : [ {
      "id" : "NAME_01",
      "firstName" : "Rashawn",
      "lastName" : "Mitchell",
      "primaryContactPhones" : [ {
        "phoneNumber" : "5174023095",
        "contactPhoneType" : "CELL_PHONE"
      } ],
      "additionalContactPhones" : [ {
        "phoneNumber" : "5174023095",
        "contactPhoneType" : "OTHER"
      } ]
    }, {
      "id" : "NAME_02",
      "firstName" : "Rashawn",
      "lastName" : "Mitchell",
      "primaryContactPhones" : [ {
        "phoneNumber" : "5174023095",
        "contactPhoneType" : "CELL_PHONE"
      } ],
      "additionalContactPhones" : [ {
        "phoneNumber" : "5174023095",
        "contactPhoneType" : "OTHER"
      } ]
    }, {
      "id" : "NAME_03",
      "firstName" : "Rashawn",
      "lastName" : "Mitchell",
      "primaryContactPhones" : [ {
        "phoneNumber" : "5174023095",
        "contactPhoneType" : "CELL_PHONE"
      } ],
      "additionalContactPhones" : [ {
        "phoneNumber" : "5174023095",
        "contactPhoneType" : "OTHER"
      } ]
    } ]
  },
  "addresses" : {
    "address" : [ {
      "id" : "ADDRESS_01",
      "addressId" : "D1a7d79ed2c",
      "unparsedAddress" : {
        "addressLine1" : "928 W EDGEWOOD BLVD UNIT 128",
        "city" : "LANSING",
        "state" : "MI",
        "zip" : "48911"
      },
      "parsedAddress" : {
        "houseNumber" : "928",
        "direction" : "W",
        "streetName" : "EDGEWOOD",
        "streetType" : "BLVD",
        "apartmentUnit" : "APT",
        "apartmentUnitNumber" : "128",
        "city" : "LANSING",
        "state" : "MI",
        "zip" : "48911",
        "rateZoneBanCode" : "551",
        "legalEntity" : "AM00",
        "buildingType" : "Y",
        "tarCode" : "LNNG",
        "rateCenterCode" : "LANSING",
        "exchangeCode" : "LNNG",
        "primaryNPANXX" : "517393",
        "clli8" : "LNNGMISO",
        "videoHubOffice" : "LNNGMI"
      },
      "additionalDetails" : {
        "additionalDetail" : [ {
          "code" : "ValidatedAddress",
          "value" : "True"
        } ]
      }
    }, {
      "id" : "ADDRESS_02",
      "unparsedAddress" : {
        "addressLine1" : "928 W EDGEWOOD BLVD",
        "addressLine2" : "UNIT 128",
        "city" : "LANSING",
        "state" : "MI",
        "zip" : "48911"
      }
    } ]
  },
  "accounts" : {
    "account" : [ {
      "id" : "ACCOUNT_01",
      "accountCategory" : "UVERSE_ACCOUNT",
      "accountSubCategory" : "EXISTING",
      "paymentArrangement" : "POSTPAID",
      "billingAccountNumber" : "252266484",
      "billingLanguagePreference" : "ENGLISH",
      "billingDetail" : [ {
        "nameReference" : "NAME_02",
        "addressReference" : "ADDRESS_02",
        "previousAddress" : "N"
      } ],
      "serviceLocationReference" : "ADDRESS_01",
      "creditCheck" : {
        "creditClass" : "HIGH",
        "creditCheckManagementTransactionId" : "U20170821716128069",
        "creditCheckRanIndicator" : true,
        "electronicIdNumber" : "U20170821716128069",
        "depositRequired" : "N",
        "safeScanAlertIndicator" : true,
        "singleCreditQueryWirelessIndicator" : false,
        "safeScanPassIndicator" : false,
        "treatmentCode" : "A001",
        "treatmentMessage" : "No additional fee is required at this time."
      },
      "billingDeliveryPreference" : "PAPERLESS",
      "accountType" : "INDIVIDUAL",
      "accountSubType" : "R",
      "passCode" : "unknown",
      "market" : "551",
      "spokenLanguagePreference" : "ENGLISH",
      "existingAutoBillStatus" : "NoExistingAutopay"
    } ]
  },
  "promotions" : {
    "promotion" : [ {
      "id" : "PROMOTION_01",
      "promotionCode" : "DV0014",
      "promotionId" : "89310366",
      "baseOfferId" : "88849634",
      "parentPricePlanCode" : "88849634",
      "componentConfigurations" : [ {
        "componentCode" : "programming",
        "componentOperations" : [ {
          "operationNames" : [ "QPRequest" ]
        }, {
          "operationNames" : [ "RQRequest" ]
        } ],
        "componentPath" : "programming",
        "componentMapRequiredIndicator" : true,
        "attributes" : [ {
          "attributeKey" : "DWSNew.ProgrammingCoreNew.ProgrammingCoreNew.RegionalOffers.RegionalOffers.BasePackageOffersParent.BasePackageOffersOptional",
          "attributeCode" : "optionKey",
          "attributeValue" : "VCNF-INSTANT-REBATE-54-12MO-V1",
          "attributeOperations" : [ {
            "operationNames" : [ "QPRequest" ]
          }, {
            "operationNames" : [ "RQRequest" ]
          } ]
        } ]
      } ],
      "promotionName" : "$54 off for 12 months ",
      "amount" : 54.00,
      "duration" : 12,
      "promotionType" : "PROMOTION",
      "promotionCycle" : "MONTHLY",
      "unitOfMeasurement" : "FLATOFF"
    }, {
      "id" : "PROMOTION_02",
      "promotionCode" : "DV1146",
      "promotionId" : "89147154",
      "baseOfferId" : "88855444",
      "parentPricePlanCode" : "88855444",
      "promotionName" : "Genie? HD DVR Discount",
      "amount" : 299.00,
      "duration" : 0,
      "promotionType" : "PROMOTION",
      "promotionCycle" : "ONETIME",
      "unitOfMeasurement" : "FLATOFF"
    }, {
      "id" : "PROMOTION_03",
      "promotionCode" : "DV1146",
      "promotionId" : "89147154",
      "baseOfferId" : "88855464",
      "parentPricePlanCode" : "88855464",
      "promotionName" : "Wireless Genie Mini Discount",
      "amount" : 99.00,
      "duration" : 0,
      "promotionType" : "PROMOTION",
      "promotionCycle" : "ONETIME",
      "unitOfMeasurement" : "FLATOFF"
    } ]
  },
  "schedulingDetails" : {
    "schedulingDetail" : [ {
      "id" : "SCHEDULINGINFO_01",
      "landlordDetail" : {
        "landlordPermission" : "N"
      },
      "nameReference" : "NAME_03",
      "actualSchedule" : {
        "selectedAppointmentDate" : "2017-08-22",
        "selectedAppointmentTime" : "08:00:00",
        "startTime" : "08:00 AM",
        "endTime" : "12:00 PM",
        "workOrderId" : "M7233009876"
      },
      "installType" : "TECH",
      "realTimeCalendarIndicator" : true
    } ]
  },
  "serviceFacilityQualifications" : {
    "serviceFacilityQualification" : [ {
      "id" : "SERVICE_QLFY_01",
      "addressReference" : "ADDRESS_01",
      "preferredNetworkType" : "FTTN",
      "profileCode" : "TDD033",
      "cpeRequiredIndicator" : false,
      "facilityCheck" : {
        "validations" : [ {
          "code" : "SC4-0000",
          "message" : "U-Verse or Non-AT&T services exist. If services are home phone & DSL, customer will need to port their Non-AT&T home phone line to AT&T then disconnect DSL with current provider. If only DSL exists, customer will need to disconnect with current provider."
        } ],
        "serviceType" : [ {
          "conflictingServiceIndicator" : true,
          "serviceType" : "U-Verse"
        } ],
        "acknowledgeIndicator" : false
      }
    } ]
  },
  "conflictingServiceDetails" : {
    "conflictingServiceDetail" : [ {
      "id" : "CONF_SRV_INFO_01",
      "addressReference" : "ADDRESS_01",
      "productDetails" : [ {
        "productDescription" : "INTERNET 25X5 DYNAMIC",
        "previousProductTransportType" : "FTTN",
        "productCode" : "UHSI",
        "packageCode" : "10005254"
      } ],
      "accountNumber" : "252266484",
      "legacyExistIndicator" : true,
      "btn" : {
        "tn" : "0000000000"
      }
    } ]
  },
  "dueAmount" : {
    "amount" : 99.00,
    "currencyType" : "USD",
    "total" : 99.00
  },
  "creditPolicy" : { },
  "partialOrderIndicator" : false,
  "salesCode" : "ALTAY7V",
  "salesLocation" : "Default",
  "agentCode" : "Z0066",
  "agentLocation" : "Z0066",
  "termsAndConditions" : {
    "termsAndConditionAccepted" : [ {
      "id" : "TC_01",
      "agreementType" : "MOBILE_ALERT",
      "agreementText" : "By entering a contact number, you authorize AT&T to call or text you with information about your AT&T services. To opt out of future communications, please contact AT&T at 1.800.288.2020. If this is a non-AT&T wireless number, text messaging rates and other charges may apply, depending on your plan and provider.",
      "accepted" : "Y",
      "timestamp" : 1503371365453
    }, {
      "id" : "TC_02",
      "agreementType" : "DIRECTV",
      "agreementText" : "\n\t\t\t\t\t\t\t&lt;p&gt;Offer for new approved residential customers only.&lt;br&gt;\n\t\t\t\t\t\t\t\t\t&lt;br&gt;YOU AGREE TO PURCHASE AND MAINTAIN 24 CONSECUTIVE MONTHS OF ANY DIRECTV BASE PROGRAMMING PACKAGE ($29.99/MO. OR ABOVE) OR QUALIFIED INTERNATIONAL SERVICE BUNDLE. IF YOU FAIL TO MAINTAIN YOUR 24-MONTH PROGRAMMING COMMITMENT, YOU AGREE THAT AN EARLY TERMINATION FEE OF $20/MONTH FOR EACH MONTH REMAINING ON YOUR AGREEMENT APPLIES.&lt;br&gt;\nIf you cancel your order prior to installation, we will issue a full refund.&lt;br&gt;\n\t\t\t\t\t\t\t\t\t\t\t\t&lt;br&gt;DIRECTV programming and pricing may vary. DIRECTV PROGRAMMING AND PRICING SUBJECT TO CHANGE AT ANY TIME.&lt;br&gt;\n\t\t\t\t\t\t\t\t\t\t\t\t\t\t&lt;br&gt;Credit or debit card used for purchase will be kept on file and may be used for any unpaid balances and fees if your DIRECTV service is disconnected.&lt;br&gt;\n\t\t\t\t\t\t\t\t\t\t\t\t\t\t\t\t&lt;br&gt;Leased equipment must be returned upon disconnect. If you do not return equipment, DIRECTV may charge a fee of $45 for each standard DIRECTV Receiver, HD Receiver, and each Genie Mini, and $135 for each DVR, HD DVR, and Genie HD DVR.&lt;br&gt;\n\t\t\t\t\t\t\t\t\t\t\t\t\t\t\t\t\t\t&lt;br&gt;You and DIRECTV agree that both parties will resolve any dispute arising under the Equipment Lease Addendum, the DIRECTV Customer Agreement or any other addendum thereto, or regarding your DIRECTV programming service, through binding arbitration as fully set forth in the DIRECTV Customer Agreement. ARBITRATION MEANS YOU WAIVE YOUR RIGHT TO A JURY TRIAL. The referenced agreements are available at &lt;a target=\"_blank\" a=\"\"\nhref=\"https://atgpreview.directv.com/DTVAPP/content/support/agreements_policies\"&gt;DIRECTV.com/agreements&lt;/a&gt;.",
      "accepted" : "Y",
      "timestamp" : 1503371365453
    } ]
  },
  "orderContact" : {
    "nameReference" : "NAME_01",
    "primaryEmailAddress" : "Rashawnmitchell92@gmail.com",
    "preferredContactMethod" : "EMAIL",
    "preferredTimeOfDayForContact" : "N/A"
  },
  "orderSource" : {
    "clientType" : "DESKTOP",
    "channel" : "CDE-HS",
    "application" : "MYATTSALES",
    "browserId" : "A004006363581",
    "additionalDetails" : {
      "additionalDetail" : [ {
        "code" : "SENDER",
        "value" : "WBFC"
      }, {
        "code" : "BUYFLOW",
        "value" : "NEWCO"
      } ]
    }
  },
  "geoAreaSingleDispatchAvailableIndicator" : true,
  "satelliteTVOnlySingleDispatchEligibleIndicator" : false,
  "singleDispatchEligibleIndicator" : true,
  "productCombinationCode" : "0",
  "encryptedIndicator" : true,
  "commonOrderIndicator" : false,
  "additionalDetails" : {
    "additionalDetail" : [ {
      "code" : "UVNADType",
      "value" : "UVRG-X"
    }, {
      "code" : "TestingOrderIndicator",
      "value" : "N"
    } ]
  }
}
```


### order


Parameter | Data Type | Required | Value Rules
--------- | --------- | -------- | -----------				
customerOrderNumber	  |	String	|	R	|	Unique apha numeric number sent by the External System identifying a particular transaction.
orderType	|	String	|	R	|	This value indicates the type of the OrderEX: CREATE
createdDate	|	Long	|	R	|	Date Order is created in buy flow, if this is not available send the submittedDate
submittedDate	|	Long	|	No	|	Date Order is submitted in buy flow in case of Create order, in case of update order, date the order is updated, can be either in buy flow or SS
[productGroups](#productgroups)	|	Array	|	R	|	This Group will contain the list of product groups in the Order
[lineitems](#lineitems)	|	Array	|	R	|	This Group will contain the list of lineitems in the Order
[names](#names)	|	Array	|	R	|	This Group will contain the list of names in the Order
[addresses](#addresses)	|	Array	|	R	|	This Group will contain the list of addresses in the Order
[accounts](#accounts)	|	Array	|	R	|	This Group will contain the list of accounts in the Order
[promotions](#promotions)	|	Array	|	O	|	This Group will contain the list of promotions in the Order
[schedulingDetails](#schedulingdetails)	|	Array	|	R	|	This Group will contain the list of schedulingdetails in the Order
[serviceFacilityQualifications](#servicefacilityqualifications)	|	Array	|	O	|	serviceFacilityQualifications rules
[conflictingServiceDetails](#conflictingservicedetails)	|	Array	|	O	|	conflictingServiceDetails
[dueAmount](#dueamount)	|	Complex	|	O	|	Due amount
partialOrderIndicator	|	boolean	|	O	|	partialOrderIndicator
salesCode	|	String	|	O	|	salesCode details
salesLocation	|	String	|	O	|	salesLocation
agentCode	|	String	|	O	|	agentCode
agentLocation	|	String	|	O	|	agentLocation
[termsAndConditions](#termsandconditions)	|	Array	|	O	|	T&Cs Details
[orderContact](#ordercontact)	|	Array	|	O	|	Contact details
[orderSource](#ordersource)	|	Array	|	O	|	Source of the order
geoArea SingleDispatch AvailableIndicator	|	boolean	|	O	|	geoAreaSingleDispatchAvailableIndicator
satelliteTVOnly SingleDispatch EligibleIndicator	|	boolean	|	O	|	satelliteTVOnlySingleDispatchEligibleIndicator
singleDispatch EligibleIndicator	|	boolean	|	O	|	singleDispatchEligibleIndicator
productCombinationCode	|	String	|	O	|	productCombinationCode
encryptedIndicator	|	boolean	|	O	|	encryptedIndicator
commonOrderIndicator	|	boolean	|	O	|	Indicates whether the Order details have to be sent to CSI COMS or not
[additionalDetails](#additionaldetails)	|	Array	|	O	|	Any additional product configuration details will be populated as code value pair under this structure


### productGroups

Parameter  | Data Type | Required | Value Rules
---------  | --------- | -------- | -----------
[group](#group)    |	Array |	No	| 1 to n : Group Record

### group

Parameter  | Data Type | Required | Value Rules
---------  | --------- | -------- | -----------
id	| String |	R	|	Unique identifier to identify a particular Product Group 
name	|	String	|	O	|	Unique name to identify a partial Product Group 
type	|	String	|	O	|	This value identifies if the group is a line of service 
sequence	|	integer	|	O	|	This value starts with 1 and indicates the sequencing of the line of services in the Order transaction 
[price](#price)	|	Array	|	O	|	This price info structure is used to identify subtotal i.e., amount and total price for an LOSG. 
[promotionReferences](#promotionreferences)	| Array	|	O	|	Indicates a promotion ref after all promotions applied. Eg: for a combined bill promotion 
[characteristics](#characteristics)	| Array |	O	|	Characteristics for Group type - line of service group (LOSG) 
[additionalDetails](#additionaldetails)	|	Array	|	O	|	

### price

Parameter  | Data Type | Required | Value Rules
---------  | --------- | -------- | -----------
amount | number | O | 
baseAmount | number | O | 
currencyType | String | O | 
installmentEligibility
msrp | number | O | 
priceType | String | O | 
[taxDetail](#taxdetail) | Array | O | 
total | number | O | 

### promotionReferences

Parameter  | Data Type | Required | Value Rules
---------  | --------- | -------- | -----------
[promotionReference](#promotionreference) | Array | R | 

### characteristics

Parameter  | Data Type | Required | Value Rules
---------  | --------- | -------- | -----------
[packageCharacteristics](#packagecharacteristics) | Array | O | 
[sharedPlanCharacteristics](#sharedplancharacteristics) | Array | O | 
[losgCharacteristics](#losgcharacteristics) | Array | O | 

### packageCharacteristics

Parameter  | Data Type | Required | Value Rules
---------  | --------- | -------- | -----------
category | String | O | 
code | String | O | 
description | String | O | 
type | String | O | 

### losgCharacteristics

Parameter  | Data Type | Required | Value Rules
---------  | --------- | -------- | -----------
losgReferenceId | String | O | 
sequence | integer | O | 
losgType | String | R | 
actionType | String | O | 
actionReason | String | O | 
productCategory | String | R | 
primaryIndicator | boolean | O | 
dealerCode | String | O | 
market | String | O | 
subMarket | String | O | 
preferredAreaCode | String | O | 
serviceArea | String | O | 
serviceAreaName | String | O | 
priceCode | String | O | 
accountReference | String | O | 
requestedExecutionDate | String | O | 
effectiveDate | String | O | 
[losgStatus](#losgstatus) | Array | O | 
serviceLocationReference | String | O | 
subscriberNameReference | String | O | 
serviceQualificationReference | String | O | 
[conflictingServiceDetailReferences](#conflictingservicedetailreferences) | Array | O | 
[termsAndConditionReferences](#termsandconditionreferences) | Array | O |
profileCode | String | O | 
schedulingDetailReference | String | O | 
[installationInstructions](#installationinstructions) | Array | O | 
[numberPortDetail](#numberportdetail) | Array | O |
installType | String | O | 
notes | String | O | 
[termsAndConditionAccepted](#termsandconditionaccepted) | Array | O | 
[voipLOSCharacteristics](#voiploscharacteristics) | Array | O | 
[direcTVLOSCharacteristics](#directvloscharacteristics) | Array | O | 
[iptvLOSCharacteristics](#iptvloscharacteristics) | Array | O | 
[internetLOSCharacteristics](#internetloscharacteristics) | Array | O | 
[wirelessLOSCharacteristics](#wirelessloscharacteristics) | Array | O | 
[addpLOSCharacteristics](#addploscharacteristics) | Array | O | 
[commonLOSCharacteristics](#commonloscharacteristics) | Array | O | 
[compensation](#compensation) | Array | O |
fulfillmentMethod | String | O | 
shippingDetailReference | String | O | 
[userDefinedLabels](#userdefinedlabels) | Array | O | 
commercePartnerCode | String | O | 
[additionalDetails](#additionaldetails) | Array | O | 


### commonLOSCharacteristics

Parameter  | Data Type | Required | Value Rules
---------  | --------- | -------- | -----------
dwellingType | String | O | 

### internetLOSCharacteristics

Parameter  | Data Type | Required | Value Rules
---------  | --------- | -------- | -----------
internetProtocolDigitalSubscriberLineAccess | String | O | 
primaryNetworkType | String | O | 
internetProgramType | String | O | 
gatewayCTN | String | O | 
gatewayCTNStatus | String | O | 
[additionalDetails](#additionaldetails) | Array | O | 


### direcTVLOSCharacteristics

Parameter  | Data Type | Required | Value Rules
---------  | --------- | -------- | -----------
serviceAgreement | String | O | 
offerLanguage | String | O | 
dealerId | String | O | 
marketingSourceCode | String | O | 
moveInOrder | String | O | 
hasMoreThanThreeFloors | boolean | O | 


### lineItems

Parameter  |  Data Type  |  Required  |  Value Rules
  -------------  |   -------------  |   -------------  |   -------------
[lineItem] (#lineitem) |  array  |  O  |  



### lineItem

Parameter  |  Data Type  |  Required  |  Value Rules
 -------------  |   -------------  |   -------------  |   -------------
id  |  string  |  O  |  
sequence  |  integer  |  O  |  
productCode  |  string  |  O  |  
productSKU  |  string  |  O  |  
productSubType  |  string  |  O  |  
billingCode  |  string  |  O  |  
socForPreviousDevice  |  string  |  O  |  
productType  |  string  |  O  |  
displayName  |  string  |  O  |  
systemName  |  string  |  O  |  
description  |  string  |  O  |  
action  |  string  |  O  |  
operation  |  string  |  O  |  
[price] (#price) |  array  |  O  |  
locationId  |  string  |  O  |  
[payments] (#payments)  |  array  |  O  |  
effectiveDate  |  long  |  O  |  
[contractDetails] (#contractdetails)  |  array  |  O  |  
quantity  |  number  |  O  |  
notes  |  string  |  O  |  
status  |  string  |  O  |  
[promotionReferences] (#promotionreferences)  |  array  |  O  |  
[groupReferences] (#groupreferences)  |  array  |  O  |  
[characteristics] (#characteristics)  |  array  |  O  |  
[hardGood] (#hardgood)  |  array  |  O  |  
[supplyChainDetail] (#supplychaindetail) |  array  |  O  |  
subscriptionId  |  string  |  O  |  
[additionalDetails] (#additionaldetails)  |  array  |  O  |  



### price

Parameter  |  Data Type  |  Required  |  Value Rules
 -------------  |   -------------  |   -------------  |   -------------
amount  |  number  |  O  |  
baseAmount  |  number  |  O  |  
currencyType  |  string  |  O  |  
installmentEligibility  |  string  |  O  |  
msrp  |  number  |  O  |  
priceType  |  string  |  O  |  
[taxDetail] (#taxdetail)  |  array  |  O  |  
total  |  number  |  O  |  



### taxDetail
 
 Parameter  |  Data Type  |  Required  |  Value Rules
 -------------  |   -------------  |   -------------  |   -------------
amount | number | O | 
[preCalculatedTax] (#precalculatedtax) | array | O | 
[lineItemTaxes] (#lineitemtaxes) | array | O | 


### preCalculatedTax

 Parameter  |  Data Type  |  Required  |  Value Rules
 -------------  |   -------------  |   -------------  |   -------------
taxableCost  |  number  |  O  |  
taxableMSRP  |  number  |  O  |  
taxableUnitPrice  |  number  |  O  |  
orderTaxAreaId  |  number  |  O  |  
shipFromTaxAreaId  |  number  |  O  |  
shipToTaxAreaId  |  number  |  O  |  
exemptionId  |  number  |  O  |  


### lineItemTaxes

 Parameter  |  Data Type  |  Required  |  Value Rules
 -------------  |   -------------  |   -------------  |   -------------
taxLineId  |  number  |  O  |  
taxCode  |  number  |  O  |  
memo  |  string  |  O  |  
printName  |  string  |  O  |  
taxable  |  string  |  O  |  
skuSpecific  |  string  |  O  |  
jurisdictionLevel  |  string  |  O  |  
jurisdictionName  |  string  |  O  |  
taxAmount  |  string  |  O  |  
taxRate  |  number  |  O  |  
taxDate  |  number  |  O  |  
[taxAuthoritiesList] (#taxauthoritieslist)  |  array  |  O  |  


 
 ### taxAuthoritiesList

  Parameter  |  Data Type  |  Required  |  Value Rules
 -------------  |   -------------  |   -------------  |   -------------
 [taxAuthorities] (#taxauthorities)  |  array  |  R  |  

 
 
 ### taxAuthorities
  Parameter  |  Data Type  |  Required  |  Value Rules
 -------------  |   -------------  |   -------------  |   -------------
taxAuthorityCode  |  string  |  R  |  
taxAuthorityValue  |  string  |  R  |  



 ### payments
  Parameter  |  Data Type  |  Required  |  Value Rules
 -------------  |   -------------  |   -------------  |   -------------
 [payment] (#payment) | array | O | 

 
 
 ### payment

  Parameter  |  Data Type  |  Required  |  Value Rules
 -------------  |   -------------  |   -------------  |   -------------
amount | number | O | 
currencyType | string | O | 
numberOfInstallment | number | O | 
paymentOptionReference | string | O | 


 
  ### contractDetails

  Parameter  |  Data Type  |  Required  |  Value Rules
 -------------  |   -------------  |   -------------  |   -------------
installmentPlanId | number | O | 
contractDisplayName | string | O | 
installmentPlanDefinition | string | O | 
annualPercentageRate | number | O | 
financeCharge | number | O | 
amountFinanced | number | O | 
balancedAmount | number | O | 
totalSalePrice | number | O | 
downPayment | number | O | 
downPaymentPercent | number | O | 
prepaidFinanceCharge | number | O | 
installmentAmount | number | O | 
installmentStatus | string | O | 
installmentType | string | O | 
contractType | string | O | 
contractSystem | string | O | 
contractSent | string | O | 
contractLength | number | O | 
equipmentInstallmentPlanIndicator | boolean | O | 

 
 
 ### promotionReferences
 
  Parameter  |  Data Type  |  Required  |  Value Rules
 -------------  |   -------------  |   -------------  |   -------------
 [promotionReference] (#promotionreference) | array | R | 

 
 
 ### groupReferences
 
  Parameter  |  Data Type  |  Required  |  Value Rules
 -------------  |   -------------  |   -------------  |   -------------
 [groupReference] (#groupreference) | array | R | 

 
 
 ### characteristics
 
  Parameter  |  Data Type  |  Required  |  Value Rules
 -------------  |   -------------  |   -------------  |   -------------
[commonCharacteristics] (#commoncharacteristics)  |  array  |  O  |  
[voipLineItemCharacteristics] (#voiplineitemcharacteristics)  |  array  |  O  |  
[direcTVLineItemCharacteristics] (#direcTVlineItemcharacteristics)  |  array  |  O  |  
[iptvLineItemCharacteristics] (#iptvlineitemcharacteristics)  |  array  |  O  |  
[internetLineItemCharacteristics] (#internetlineitemcharacteristics)  |  array  |  O  |  
[addOnSolutionCharacterstics] (#addonsolutioncharacterstics)  |  array  |  O  |  
[wirelessLineItemCharacteristics] (#wirelesslineitemcharacteristics)  |  array  |  O  |  

 
 
 ### commonCharacteristics
 
  Parameter  |  Data Type  |  Required  |  Value Rules
 -------------  |   -------------  |   -------------  |   -------------
[componentConfigurations] (#componentconfigurations)  |  array  |  O  |  
requestComponentGroup  |  string  |  O  |  
ignorePricePlanCode  |  string  |  O  |  
productSpecificationId  |  string  |  O  |  
[fees] (#fees)  |  array  |  O  |  
 
 
 
 ###  componentConfigurations

  Parameter  |  Data Type  |  Required  |  Value Rules
 -------------  |   -------------  |   -------------  |   -------------
componentCode  |  string  |  O  |  
[componentOperations] (#componentoperations)  |  array  |  O  |  
componentPath  |  string  |  O  |  
componentMapRequiredIndicator  |  boolean  |  O  |  
[attributes] (#attributes)  |  array  |  O  |  

 
 
 ### componentOperations
 
  Parameter  |  Data Type  |  Required  |  Value Rules
 -------------  |   -------------  |   -------------  |   -------------
 [operationNames] (#operationnames)  |  array  |  R  |  


 
 ### attributes

  Parameter  |  Data Type  |  Required  |  Value Rules
 -------------  |   -------------  |   -------------  |   -------------
attributeKey  |  string  |  O  |  
attributeCode  |  string  |  O  |  
attributeValue  |  string  |  O  |  
[attributeOperations] (#attributeoperations)  |  array  |  O  |  

 
 
 ### attributeOperations
 
  Parameter  |  Data Type  |  Required  |  Value Rules
 -------------  |   -------------  |   -------------  |   -------------
  [operationNames] (#operationnames)  |  array  |  R  |
  
  
  
 ### fees

  Parameter  |  Data Type  |  Required  |  Value Rules
 -------------  |   -------------  |   -------------  |   -------------
feeId  |  string  |  O  |  
feeIdType  |  string  |  O  |  
waivedIndicator  |  boolean  |  O  |  
waivedReason  |  string  |  O  |  

 
 
 ### voipLineItemCharacteristics

  Parameter  |  Data Type  |  Required  |  Value Rules
 -------------  |   -------------  |   -------------  |   -------------
callerId  |  string  |  O  |  
uverseMessaging  |  string  |  R  | 

 
 
 ###  internetLineItemCharacteristics
 
   Parameter  |  Data Type  |  Required  |  Value Rules
 -------------  |   -------------  |   -------------  |   -------------
bucketAllowance  |  string  |  O  |  
overageBucketAllowance  |  string  |  O  |  
pricePerBucketAllowance  |  number  |  O  |  
maxOverageCharge  |  number  |  O  |  
planDownloadSpeed  |  string  |  O  |  
boltOnType  |  string  |  O  |  
ipType  |  string  |  O  |  

 
 
 ### addOnSolutionCharacterstics
 
   Parameter  |  Data Type  |  Required  |  Value Rules
 -------------  |   -------------  |   -------------  |   -------------
domainRegistration  |  string  |  O  |  
domainName  |  string  |  O  |  
registrationType  |  string  |  O  |  
parentItem  |  string  |  O  |  

 
 
 ### wirelessLineItemCharacteristics

   Parameter  |  Data Type  |  Required  |  Value Rules
 -------------  |   -------------  |   -------------  |   -------------
partnerCode  |  string  |  O  |  
distributionChannelId  |  string  |  O  |  
newSalesChannelId  |  string  |  O  |  
[tradeInDetail] (#tradeindetail)  |  array  |  O  |  
nciEligibleIndicator  |  boolean  |  O  |  
offerType  |  string  |  O  |  
availabilityType  |  string  |  O  |  
[packetDataProtocol] (#packetdataprotocol)  |  array  |  O  |  
[attDynamicTrafficManager] (#attdynamictrafficmanager)  |  array  |  O  |  
omniReferenceNumber  |  string  |  O  |  
omniRequestStatus  |  string  |  O  |  

 
 
 ### tradeInDetail
 
   Parameter  |  Data Type  |  Required  |  Value Rules
 -------------  |   -------------  |   -------------  |   -------------
claimId  |  string  |    |  
exchangeType  |  string  |    |  
installmentPlanId  |  string  |    |  
deviceClearingAgreement  |  string  |    |  
nonComplianceFee  |  number  |    |  
payupAmount  |  number  |    |  

 
 
### packetDataProtocol

   Parameter  |  Data Type  |  Required  |  Value Rules
 -------------  |   -------------  |   -------------  |   -------------
packetDataProtocolType  |  string  |  O  |  
ipAddress  |  string  |  O  |  
ipv6Address  |  string  |  O  |  
ipversionType  |  string  |  O  |  
ltePacketDataProtocolIndicator  |  boolean  |  O  |  
defaultPacketDataProtocolIndicator  |  boolean  |  O  |  
onlineChargingSystemIndicator  |  boolean  |  O  |  
apnName  |  string  |  O  |  
[additionalDetails] (#additionaldetails)  |  array  |  O  |  

  
 
### additionalDetails

   Parameter  |  Data Type  |  Required  |  Value Rules
 -------------  |   -------------  |   -------------  |   -------------
 [additionalDetail] (#additionaldetail)  |  array  |  R  |  

 
  
  ### additionalDetail
 
   Parameter  |  Data Type  |  Required  |  Value Rules
 -------------  |   -------------  |   -------------  |   -------------
type  |  string  |  O  |  
parentType  |  string  |  O  |  
code  |  string  |  R  |  
value  |  string  |  R  |  

 
 
  attDynamicTrafficManager
 
   Parameter  |  Data Type  |  Required  |  Value Rules
 -------------  |   -------------  |   -------------  |   -------------
manifestURL  |  string  |  O  |  
enterpriseId  |  string  |  O  |  
manifestLabel  |  string  |  O  |  
[additionalDetails] (#additionaldetails)  |  array  |  O  |  



### additionalDetails

   Parameter  |  Data Type  |  Required  |  Value Rules
 -------------  |   -------------  |   -------------  |   -------------
 [additionalDetail] (#additionaldetail)  |  array  |  R  |  
 
 
 
 ### additionalDetail
 
  Parameter  |  Data Type  |  Required  |  Value Rules
 -------------  |   -------------  |   -------------  |   -------------
type  |  string  |  O  |  
parentType  |  string  |  O  |  
code  |  string  |  R  |  
value  |  string  |  R  |  
 
 
 
### hardGood

   Parameter  |  Data Type  |  Required  |  Value Rules
 -------------  |   -------------  |   -------------  |   -------------
byodIndicator  |  boolean  |  O  |  
hardGoodType  |  string  |  O  |  
productImageUrl  |  string  |  O  |  
make  |  string  |  O  |  
model  |  string  |  O  |  
manufacturerCode  |  string  |  O  |  
serialNumber  |  string  |  O  |  
fieldId  |  string  |  O  |  
deliveryPromiseNoteEnglish  |  string  |  O  |  
deliveryPromiseNoteSpanish  |  string  |  O  |  
preOrderIndicator  |  boolean  |  O  |  
availabilityDate  |  long  |  O  |  
shippedHotIndicator  |  boolean  |  O  |  
[shipmentCommitDate] (#shipmentcommitdate)  |  array  |  O  |  
[deliveryByDate] (#deliverybydate)  |  array  |  O  |  
networkAccessDeviceType  |  string  |  O  |  
cardSerialNumber  |  string  |  O  |  
eid  |  string  |  O  |  
iccId  |  string  |  O  |  
whiteGloveDeliveryPartner  |  string  |  O  |  
[wirelessHardGoodCharacteristics] (#wirelesshardgoodcharacteristics)  |  array  |  O  |  



 ### shipmentCommitDate
 
 Parameter  |  Data Type  |  Required  |  Value Rules
 -------------  |   -------------  |   -------------  |   -------------
fromDate  |  long  |  O  |  
toDate  |  long  |  O  |  


 
 ### deliveryByDate
 
 Parameter  |  Data Type  |  Required  |  Value Rules
 -------------  |   -------------  |   -------------  |   -------------
fromDate  |  long  |  O  |  
toDate  |  long  |  O  |  



 ### wirelessHardGoodCharacteristics
 
   Parameter  |  Data Type  |  Required  |  Value Rules
 -------------  |   -------------  |   -------------  |   -------------
techType  |  string  |  O  |  
equipmentType  |  string  |  O  |  
imei  |  string  |  O  |  
imeiType  |  string  |  O  |  
internationalMobileSubscriberIdentity  |  string  |  O  |  
usoc  |  string  |  O  |  
connectionType  |  string  |  O  |  
zodiacSequenceNumber  |  string  |  O  |  
equipmentUpgrade  |  string  |  O  |  
phoneType  |  string  |  O  |  
deviceCategory  |  string  |  O  |  

 
 
 ### supplyChainDetail

  Parameter  |  Data Type  |  Required  |  Value Rules
 -------------  |   -------------  |   -------------  |   -------------
availabilityDate  |  string  |  O  |  
[orderDocumentDetail] (#orderdocumentdetail)  |  array  |  O  |  
quantityOrdered  |  number  |  O  |  
quantityBackOrdered  |  number  |  O  |  
quantityCanceled  |  number  |  O  |  
quantityShipped  |  number  |  O  |  
quantityToShip  |  number  |  O  |  
price  |  number  |  O  |  
exchangeOrderId  |  string  |  O  |  
exchangeDocumentId  |  string  |  O  |  
trackingNumber  |  string  |  O  |  
carrier  |  string  |  O  |  
shippedDate  |  long  |  O  |  
claimRMANumber  |  string  |  O  |  

 
 
 ### orderDocumentDetail
 
 Parameter  |  Data Type  |  Required  |  Value Rules
 -------------  |   -------------  |   -------------  |   -------------
location  |  string  |  O  |  
activity  |  string  |  O  |  
orderId  |  string  |  O  |  

 
 
 ### additionalDetails

  Parameter  |  Data Type  |  Required  |  Value Rules
 -------------  |   -------------  |   -------------  |   -------------
 [additionalDetail] (#additionaldetail)  |  array  |  R  |  
 
 
 
 ### additionalDetail
 
 Parameter  |  Data Type  |  Required  |  Value Rules
 -------------  |   -------------  |   -------------  |   -------------
type  |  string  |  O  |  
parentType  |  string  |  O  |  
code  |  string  |  R  |  
value  |  string  |  R  |  




### names

Parameter  | Data Type | Required | Value Rules
---------  | --------- | -------- | -----------
[name](#name) | Array | R | 

### name

Parameter  | Data Type | Required | Value Rules
---------  | --------- | -------- | -----------
id | String | R | 
firstName | String | O | 
lastName | String | O | 
[primaryContactPhones](#primarycontactphones) | Array | O | 

### primaryContactPhones

Parameter  | Data Type | Required | Value Rules
---------  | --------- | -------- | -----------
phoneNumber | String | R | 
contactPhoneType | String | O | 

### contactPhoneType

Parameter  | Data Type | Required | Value Rules
---------  | --------- | -------- | -----------
enum | String | O | 

### addresses

Parameter  | Data Type | Required | Value Rules
---------  | --------- | -------- | -----------
[address](#address) | Array | R | 

### address

Parameter  | Data Type | Required | Value Rules
---------  | --------- | -------- | -----------
id | String | O | 
addressId | String | O | 
[unparsedAddress](#unparsedaddress) | Array | O | 
[parsedAddress](#parsedaddress) | Array | O | 
[additionalDetails](#additionaldetails)	|	Array	|	O	| 

### unparsedAddress

Parameter  | Data Type | Required | Value Rules
---------  | --------- | -------- | -----------
addressLine1 | String | R | 
city | String | R | 
state | String | R | 
zip | String | R | 

### parsedAddress

Parameter  | Data Type | Required | Value Rules
---------  | --------- | -------- | -----------
houseNumber | String | O | 
direction | String | O | 
streetName | String | O | 
streetType | String | O | 
apartmentUnit | String | O | 
apartmentUnitNumber | String | O | 
city | String | R | 
state | String | R | 
zip | String | R | 
rateZoneBanCode | String | O | 
legalEntity | String | O | 
buildingType | String | O | 
tarCode | String | O | 
rateCenterCode | String | O | 
exchangeCode | String | O | 
primaryNPANXX | String | O | 
clli8 | String | O | 
videoHubOffice | String | O | 


### accounts

Parameter  | Data Type | Required | Value Rules
---------  | --------- | -------- | -----------
[account](#account) | Array | R | 

### account

Parameter  | Data Type | Required | Value Rules
---------  | --------- | -------- | -----------
id | String | R| 
sequence | integer | O | 
accountCategory | String | O | 
accountSubCategory | String | O | 
paymentArrangement | String | O | 
billingAccountNumber | String | O | 
businessAccountName | String | O | 
primaryCTN | String | O | 
billingLanguagePreference | String | O | 
billingAccountTelephoneNumber | String | O | 
[billingDetail](#billingdetail) | Array | O | 
serviceLocationReference | String | O | 
businessAddressReference | String | O | 
anchorCTN | String | O | 
targetCTN | String | O | 
ctnValidatedIndicator | boolean | O | 
[creditCheck](#creditcheck) | Array | O | 
[bankingPartner](#bankingpartner) | Array | O | 
[creditAlert](#crediaAlert) | Array | O | 
billingDeliveryPreference | String | O | 
[electronicLetterOfAuthorization](#electronicLetterofauthorization) | Array | O | 
bigData | String | O | 
gigaPower | String | O | 
[contractAcceptance](#contractacceptance) | Array | O | 
[unifiedAccount](#unifiedaccount) | Array | O | 
liabilityType | String | O | 
delinquentAccountIndicator | boolean | O | 
accountType | String | O | 
accountSubType | String | O | 
enterpriseType | String | O | 
b2bReference | String | O | 
passCode | String | O | 
langId | String | O | 
ebillReason | String | O | 
landLineNumber | String | O | 
customerCode | String | O | 
consentToCCIndicator | boolean | O | 
market | String | O | 
subMarket | String | O | 
priceCode | String | O | 
spokenLanguagePreference | String | O | 
accountCrossmarketIndicator | boolean | O | 
[provisioningSystems](#provisioningsystems) | Array | O | 
existingAutoBillStatus | String | O | 
winBackIndicator | boolean | O | 
thirdPartyCombinedBill | String | O | 
[additionalDetails](#additionaldetails) | Array | O | 
cpni | boolean | O | 
[mdmProfileSetting](#mdmprofilesetting) | Array | O | 

### accountCategory
Parameter  | Data Type | Required | Value Rules
---------  | --------- | -------- | -----------
enum | String | O | 

### accountSubCategory
Parameter  | Data Type | Required | Value Rules
---------  | --------- | -------- | -----------
enum | String | O | 

### paymentArrangement
Parameter  | Data Type | Required | Value Rules
---------  | --------- | -------- | -----------
enum | String | O | 

### billingLanguagePreference
Parameter  | Data Type | Required | Value Rules
---------  | --------- | -------- | -----------
enum | String | O | 

### billingDetail
Parameter  | Data Type | Required | Value Rules
---------  | --------- | -------- | -----------
nameReference | String | O | 
addressReference | String | O | 
previousAddress | String | O | 

### creditCheck
Parameter  | Data Type | Required | Value Rules
---------  | --------- | -------- | -----------
creditClass | String | O | 
creditCheckManagementTransactionId | String | O | 
creditCheckRanIndicator | boolean | O | 
electronicIdNumber | String | O | 
depositRequired | String | O | 
safeScanAlertIndicator | boolean | O | 
singleCreditQueryWirelessIndicator | boolean | O | 
safeScanPassIndicator | boolean | O | 
treatmentCode | String | O | 
treatmentMessage | String | O | 


### promotions

Parameter  | Data Type | Required | Value Rules
---------  | --------- | -------- | -----------
[promotion](#promotion) | Array | R | 

### promotion

Parameter  | Data Type | Required | Value Rules
---------  | --------- | -------- | -----------
id | String | R| 
promotionCode | String | O | 
promotionId | String | O | 
displayLevel | String | O | 
sequence | integer | O | 
baseOfferId | String | O | 
parentPricePlanCode | String | O | 
[componentConfigurations](#componentconfigurations) | Array | O | 
promotionName | String | O | 
amount | Number | O | 
percent | Number | O | 
fixedAmount | Number | O | 
duration | Number | O | 
promotionType | String | O | 
promotionCycle | String | O | 
unitOfMeasurement | String | O | 
effectiveInDays | Number | O | 
complexDiscountIndicator | boolean | O | 
couponCode | String | O | 
[qualifyingServiceDetails](#qualifyingservicedetails) | Array | O | 
ioSequence | String | O | 
promotionBillingCode | String | O | 
[additionalDetails](#additionaldetails)	|	Array	|	O	|	

### displayLevel
Parameter  | Data Type | Required | Value Rules
---------  | --------- | -------- | -----------
enum | String | O | 

### componentConfigurations

Parameter  | Data Type | Required | Value Rules
---------  | --------- | -------- | -----------
componentCode | String | O | 
[componentOperations](#componentoperations) | Array | O | 
componentPath | String | O | 
componentMapRequiredIndicator | boolean | O | 
[attributes](#attributes) | Array | O | 
	
### componentOperations

Parameter  | Data Type | Required | Value Rules
---------  | --------- | -------- | -----------
[operationNames](#operationnames) | Array | R | 


### attributes

Parameter  | Data Type | Required | Value Rules
---------  | --------- | -------- | -----------
attributeKey | String | O | 
attributeCode | String | O | 
attributeValue | String | O | 
[attributeOperations](#attributeoperations) | Array | O | 

### attributeOperations

Parameter  | Data Type | Required | Value Rules
---------  | --------- | -------- | -----------
[operationNames](#operationnames) | Array | R | 

### qualifyingServiceDetails

Parameter  | Data Type | Required | Value Rules
---------  | --------- | -------- | -----------
id | String | O | 
qualificationServiceType | String | O | 
[qualifyingAttributeDetails](#qualifyingattributedetails) | Array | O | 

### qualifyingAttributeDetails

Parameter  | Data Type | Required | Value Rules
---------  | --------- | -------- | -----------
id | String | O | 
qualificationAttributeName | String | O | 
qualificationAttributeValue | String | O | 

### promotionType
Parameter  | Data Type | Required | Value Rules
---------  | --------- | -------- | -----------
enum | String | O | 

### promotionCycle
Parameter  | Data Type | Required | Value Rules
---------  | --------- | -------- | -----------
enum | String | O | 

### unitOfMeasurement
Parameter  | Data Type | Required | Value Rules
---------  | --------- | -------- | -----------
enum | String | O | 

### schedulingDetails

Parameter  | Data Type | Required | Value Rules
---------  | --------- | -------- | -----------
[schedulingDetail](#schedulingdetail) | Array | R | 

### schedulingDetail

Parameter  | Data Type | Required | Value Rules
---------  | --------- | -------- | -----------
id | String | R | 
[landlordDetail](#landlorddetail) | Array | O | 
[connecTechInstallationOptions](#connectechinstallationoptions) | Array | O |
nameReference | String | O | 
[actualSchedule](#actualschedule) | Array | R | 
[scheduleByDayAndTime](#schedulebydayandtime) | Array | R | 
scheduleAsSoonAsPossibleIndicator | boolean | R | 
billingInstallmentsIndicator | boolean | O | 
appointmentComment | String | O | 
installType | String | O | 
reservationId | String | O | 
eventCode | String | O | 
eventCodeEnteredManuallyIndicator | boolean | O | 
realTimeCalendarIndicator | boolean | O | 
bestTimeToReach | String | O | 
[additionalDetails](#additionaldetails)	| Array	| O	|	


### landlordDetail

Parameter  | Data Type | Required | Value Rules
---------  | --------- | -------- | -----------
landlordName | String | O | 
landlordPhoneNumber | String | O | 
landlordPermission | String | O | 

### landlordPermission
Parameter  | Data Type | Required | Value Rules
---------  | --------- | -------- | -----------
enum | String | O | Y/N value


### connecTechInstallationOptions

Parameter  | Data Type | Required | Value Rules
---------  | --------- | -------- | -----------
connecTechInstallationOption | String | O | 
connecTechServiceDate | String | O | 

### connecTechInstallationOption
Parameter  | Data Type | Required | Value Rules
---------  | --------- | -------- | -----------
enum | String | O | 


### actualSchedule

Parameter  | Data Type | Required | Value Rules
---------  | --------- | -------- | -----------
selectedAppointmentDate | String | O | 
selectedAppointmentTime | String | O | 
startTime | String | O | 
endTime | String | O | 
workOrderId | String | O | 

### scheduleByDayAndTime

Parameter  | Data Type | Required | Value Rules
---------  | --------- | -------- | -----------
monday | String | O | 
tuesday | String | O | 
wednesday | String | O | 
thursday | String | O | 
friday | String | O | 
saturday | String | O | 
sunday | String | O | 
anyDayOfTheWeek | String | R | 

### serviceFacilityQualifications

Parameter  | Data Type | Required | Value Rules
---------  | --------- | -------- | -----------
[serviceFacilityQualification](#servicefacilityqualification) | Array | O | 

### serviceFacilityQualification

Parameter  | Data Type | Required | Value Rules
---------  | --------- | -------- | -----------
id | String | R | 
addressReference | String | O | 
preferredNetworkType | String | O | 
profileCode | String | O | 
frequency17MhzIndicator | boolean | O | 
vectoringIndicator | boolean | O | 
cpeRequiredIndicator | boolean | O | 
[facilityCheck](#facilitycheck) | Array | O | 
potsAvailableIndicator | boolean | O | 
dslAvailableIndicator | boolean | O | 

### facilityCheck

Parameter  | Data Type | Required | Value Rules
---------  | --------- | -------- | -----------
[validations](#validations) | Array | O | 
[serviceType](#servicetype) | Array | O | 
acknowledgeIndicator | boolean | O | 

### validations

Parameter  | Data Type | Required | Value Rules
---------  | --------- | -------- | -----------
code | String | O | 
message | String | O | 

### serviceType

Parameter  | Data Type | Required | Value Rules
---------  | --------- | -------- | -----------
conflictingServiceIndicator | boolean | O | 
serviceType | String | O | 

### conflictingServiceDetails

Parameter  | Data Type | Required | Value Rules
---------  | --------- | -------- | -----------
[conflictingServiceDetail](#conflictingservicedetail) | Array | O | 

### conflictingServiceDetail

Parameter  | Data Type | Required | Value Rules
---------  | --------- | -------- | -----------
id | String | R | 
addressReference | String | O | 
[productDetails](#productdetails) | Array | O | 
accountNumber | String | O | 
changeType | String | O | 
disconnectNumber | String | O | 
customerCode | String | O | 
legacyExistIndicator | boolean | O | 
[btn](#btn) | Array | O | 
disconnectDate | String | O | 
region | String | O | 
state | String | O | 
referallOfCallsIndicator | boolean | O | 
[dslmemberDetail](#dslmemberdetail) | Array | 

### productDetails

Parameter  | Data Type | Required | Value Rules
---------  | --------- | -------- | -----------
productDescription | String | O | 
action | String | O | 
previousProductTransportType | String | O | 
productCode | String | O | 
packageCode | String | O | 

### btn

Parameter  | Data Type | Required | Value Rules
---------  | --------- | -------- | -----------
paymentAmount | nunmber | O | 
customerCode | String | O | 
tn | String | O | 

### regio

Parameter  | Data Type | Required | Value Rules
---------  | --------- | -------- | -----------
enum | String | O |	

### state

Parameter  | Data Type | Required | Value Rules
---------  | --------- | -------- | -----------
enum | String | O |	

### dslmemberDetail

Parameter  | Data Type | Required | Value Rules
---------  | --------- | -------- | -----------
memberId | String | O | 
authenticatedIndicator | boolean | O | 
reuseDSLMemberIdIndicator | boolean | O | 


### dueAmount

Parameter  | Data Type | Required | Value Rules
---------  | --------- | -------- | -----------
amount | number | O | 
baseAmount | number | O | 
currencyType | String | O | Currency Type
installmentEligibility | String | O | 
msrp | number | O | 
priceType | String | O | 
[taxDetail](#taxdetail) | Array | O | 
total | number | O | 

### currencyType

Parameter  | Data Type | Required | Value Rules
---------  | --------- | -------- | -----------
enum | String | O |	USD

### installmentEligibility

Parameter  | Data Type | Required | Value Rules
---------  | --------- | -------- | -----------
enum | String | O |	Y/N value for eligibility for installments

### priceType

Parameter  | Data Type | Required | Value Rules
---------  | --------- | -------- | -----------
enum | String | O |	Type of pricing for ex RC, NRC etc

### taxDetail

Parameter  | Data Type | Required | Value Rules
---------  | --------- | -------- | -----------
amount | number | O | 
[preCalculatedTax](#precalculatedtax) | Array | O | 
[lineItemTaxes](#lineitemtaxes) | Array | O |

### preCalculatedTax

Parameter  | Data Type | Required | Value Rules
---------  | --------- | -------- | -----------
taxableCost | number | O | 
taxableMSRP | number | O | 
taxableUnitPrice | number | O | 
orderTaxAreaId | number | O | 
shipFromTaxAreaId | number | O | 
shipToTaxAreaId | number | O | 
exemptionId | number | O | 

### lineItemTaxes

Parameter  | Data Type | Required | Value Rules
---------  | --------- | -------- | -----------
taxLineId | number | O | 
taxCode | String | O | 
memo | String | O | 
printName | String | O | 
taxable | String | O | 
skuSpecific | String | O | 
jurisdictionLevel | String | O | 
jurisdictionName | String | O | 
taxAmount | number | O | 
taxRate | number | O | 
taxDate | String | O | 
[taxAuthoritiesList](#taxauthoritieslist) | Array | O | 
 
### taxAuthoritiesList

Parameter  | Data Type | Required | Value Rules
---------  | --------- | -------- | -----------
[taxAuthorities](#taxAuthorities) | Array | R | 

### taxAuthorities

Parameter  | Data Type | Required | Value Rules
---------  | --------- | -------- | -----------
taxAuthorityCode | String | R | 
taxAuthorityValue | number | R | 

### termsAndConditions

Parameter  | Data Type | Required | Value Rules
---------  | --------- | -------- | -----------
[termsAndConditionAccepted](#termsandconditionsaccepted) | Array | R | 
 
### termsAndConditionAccepted

Parameter  | Data Type | Required | Value Rules
---------  | --------- | -------- | -----------
id | String | R | 
agreementType | String | O | Type of agreement (for products)
agreementText | String | O | Text of agreement
accepted | String | R |  Customer acceptance indicator
timestamp | String | O | 
version | String | O | 
orderLevelIndicator | boolean | O | TC's at order level

### agreementType

Parameter  | Data Type | Required | Value Rules
---------  | --------- | -------- | -----------
enum | String | O |	Type of agreement (for products)

### accepted

Parameter  | Data Type | Required | Value Rules
---------  | --------- | -------- | -----------
enum | String | O |	Y/N value for TC acceptance


### orderContact

Parameter  | Data Type | Required | Value Rules
---------  | --------- | -------- | -----------
nameReference | String | R | Customer name
primaryEmailAddress | String | R | Primary contact email
secondaryEmailAddress | String | O | Secondary contact email
additionalEmailRecipients | String | O | Additonal contact email
preferredContactMethod | String | O | Modes for contacting customer
preferredTimeOfDayForContact | String | O | Best time to contact customer
orderConfirmationByEmailPermissionIndicator | boolean | O | Permission to send the order confirmation email
[additionalDetails](#additionaldetails)	|	Array	|	O	|	Any additional contact details will be populated as code value pair under this structure

### preferredContactMethod

Parameter  | Data Type | Required | Value Rules
---------  | --------- | -------- | -----------
enum | String | O |	Modes for contacting customer 


### orderSource

Parameter  | Data Type | Required | Value Rules
---------  | --------- | -------- | -----------
channel | String | R | Order Source Channel
salesChannelType | String | O| 
application | String | R | Order Source Application
sequence | number | O | 
[additionalDetails](#additionaldetails)	|	Array	|	O	|	Any additional order source details will be populated as code value pair under this structure


### additionalDetails

Parameter  | Data Type | Required | Value Rules
---------  | --------- | -------- | -----------
type | String | O | 
parentType | String | O | 
code | String | O| 
value | String | O |  


> The above command returns JSON structured like this:

```json
{
  "application": "MYATTSALES",
  "channel": "DE-MOBILITY",
  "customerOrderNumber": "22-137578111080706"
}
```

# InquireOrder API 

### HTTP(s) Request  to retrieve the order by BAN/CTN

`GET http(s)://host:port/restservice/inquire?[ban][ctn]=1234567891`

### Query Parameters

Parameter | Required | Description
--------- | ------- | -----------
BAN/CTN  | yes | BAN/CTN no of the order

> http://host:port/restservice/inquire?ban=1234567891
  

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




