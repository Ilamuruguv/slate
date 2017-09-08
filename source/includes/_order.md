# order

Parameter | Data Type | Required | Value Rules
--------- | --------- | -------- | -----------				
customerOrderNumber	  |	String	|	R	|	Unique apha numeric number sent by the External System identifying a particular transaction.
orderType	|	String	|	R	|	This value indicates the type of the OrderEX: CREATE
createdDate	|	Long	|	R	|	Date Order is created in buy flow, if this is not available send the submittedDate
submittedDate	|	Long	|	No	|	Date Order is submitted in buy flow in case of Create order, in case of update order, date the order is updated, can be either in buy flow or SS
[productGroups](#productgroups)	|	Array	|	R	|	This Group will contain the list of product groups in the Order
[lineitems](#lineitems)	|	Array	|	R	|	This Group will contain the list of lineitems in the Order
[Names](#names)	|	Array	|	R	|	This Group will contain the list of names in the Order
[Addresses](#addresses)	|	Array	|	R	|	This Group will contain the list of addresses in the Order
[accounts](#accounts)	|	Array	|	R	|	This Group will contain the list of accounts in the Order
[promotions](#promotions)	|	Array	|	O	|	This Group will contain the list of promotions in the Order
[schedulingDetails](#schedulingdetails)	|	Array	|	R	|	This Group will contain the list of schedulingdetails in the Order
[serviceFacilityQualifications](#servicefacilityqualifications)	|	Array	|	O	|	serviceFacilityQualifications rules
[conflictingServiceDetails](#conflictingservicedetails)	|	Array	|	O	|	conflictingServiceDetails
[dueamount](#dueamount)	|	Complex	|	O	|	Due amount
partialOrderIndicator	|	boolean	|	O	|	partialOrderIndicator
salesCode	|	String	|	O	|	salesCode details
salesLocation	|	String	|	O	|	salesLocation
agentCode	|	String	|	O	|	agentCode
agentLocation	|	String	|	O	|	agentLocation
[termsAndConditions](#termsandconditions)	|	Array	|	O	|	T&Cs Details
[orderContact](#ordercontact)	|	Array	|	O	|	Contact details
[orderSource](#ordersource)	|	Array	|	O	|	Source of the order
geoAreaSingleDispatchAvailableIndicator	|	boolean	|	O	|	geoAreaSingleDispatchAvailableIndicator
satelliteTVOnlySingleDispatchEligibleIndicator	|	boolean	|	O	|	satelliteTVOnlySingleDispatchEligibleIndicator
singleDispatchEligibleIndicator	|	boolean	|	O	|	singleDispatchEligibleIndicator
productCombinationCode	|	String	|	O	|	productCombinationCode
encryptedIndicator	|	boolean	|	O	|	encryptedIndicator
commonOrderIndicator	|	boolean	|	O	|	Indicates whether the Order details have to be sent to CSI COMS or not
[additionalDetails](#additionaldetails)	|	Array	|	O	|	Any additional product configuration details will be populated as code value pair under this structure

