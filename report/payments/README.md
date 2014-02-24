GET /reports/payments/{id}
=======

Returns reporting data pertaining to payments

### Common API Components

[See Common API Components](../../../../blob/master/Common.md)

### Example Request

```bash
curl https://api.chathamfinancial.com/reports/payments/exampleReport?fromdate=2013-10-31&todate=2013-11-30&offset=0
    -X GET
	-H "Authorization: Bearer XXX"
```

### Example Response

```json
{
    "Paging": {
        "Limit": 500,
        "Offset": 0,
        "TotalRecords": 2
    },
    "Items": [{
            "Id": "23433234",
            "TransactionId": "CFSponsor20130930",
            "PaymentAmount": 10000000,
            "PaymentDate": "2013-10-31"
		},
        {
            "Id": "23433235",
            "TransactionId": "CFSponsor20130930",
            "PaymentAmount": 10000000,
            "PaymentDate": "2013-11-30"
    	},
        ,
        {
            "Id": "1343435",
            "TransactionId": "CFSponsor20120831",
            "PaymentAmount": 10000000,
            "PaymentDate": "2013-10-31"
        },
        
	]	
}
```

### Request Query String Parameters

| Parameter     | Type      |  Required  | Description                      |
| ------------- | --------- | :--------: | -------------------------------- |
| fromdate      | `datetime`  | Yes        | A date in the format YYYY-MM-DD. |
| todate        | `datetime`  | Yes        | A date in the format YYYY-MM-DD. |


### Response Codes

|  Status Code  | Description
| :-----------: | -----------
| 200           | The transaction data is returned.
| 400           | Parameter validation failed. Check the response body for details. 
| | Examples: 
| | - Invalid Column name  
| | - From Date is not in the specified Date format
| | - To Date is not in the specified Date format
| 401           | Missing, invalid, expired or revoked access token.
| 500           | Transaction data gathering failed. Try again or contact support if you continue to receive this response.


### Supported Transaction Data Fields

<br><br>

| Field Name    | Example Value  | Description    | Swap   | Cap/Floor   | Collar | Swaption    | Cross Currency Swap | FX Spot | FX Fwd | FX Option | FX Collar
| :-----------: | -------------- | -------------- | ------ | ----------- | ------ | ----------- | ------------------- | ------- | ------ | --------- | -------------- 
| ReportStartDate | 2013-10-31T00:00:00.0000000-04:00 | The start date specified for the report.
| ReportEndDate | 2013-11-30T00:00:00.0000000-05:00 | The end date specified for the report.
| ReportCreationDateTime | 2014-01-23T10:54:59.5030895-05:00 | Date and time when the report was created (run).
| TradeCreationDateTime | 2013-07-31T16:34:02.7430000-04:00 | Date and time when transaction was created in ChathamDirect. If using the transaction loader, 'TradeCreationDateTime' and 'TradeInputCompleteDate' will share the same date.
| TradeCreator | Wes Millard | Full name of the user that created the transaction. If using the transaction loader, this is the user that uploaded the input file.
| TradeInputCompleteDate | 2013-09-23T04:00:00.0000000Z | Date when the transaction was activated in ChathamDirect (this is not the same as the 'TradeDateTime'). If using the transaction loader, 'TradeCreationDateTime' and 'TradeInputCompleteDate' will share the same date. When loaded manually by Chatham, 'TradeInputCompleteDate' may occur after 'TradeCreationDateTime'.
| TradeInputter | Joe Smith | Full name of user that activated the transaction in ChathamDirect (completed input of all appropriate fields). If using the transaction loader, the system is considered the 'TradeInputer'. If loaded manually by Chatham, 'TradeInputer' will be the Chatham employee who activated the trade.
| MatchStatus | Matched | Current status of transaction matching (confirmation), whether performed manually or through a trade affirmation platform such as Misys.
| MatchRequestDateTime | 2013-07-31T16:34:02.7430000-04:00 | Date and time when transaction matching (confirmation) was initiated by Chatham or client. 'ConfirmCheckDate' is the date when matching was completed.
| MatchRequestor | Daniel Sweeney | Full name of the user that initiated the matching request.
| ConfirmCheckDate | 2013-09-23T04:00:00.0000000Z | Date when the Confirm Check action in ChathamDirect was designated as complete for this trade Returns null if not confirmed.
| ConfirmChecker | Joe Smith | Name of user that designated the Confirm Check action in ChathamDirect as complete – should return null if not confirmed. 
| LastModificationDateTime | 2013-09-23T04:00:00.0000000Z | Date when a material economic or descriptive field was last modified.
| LastModifier | Joe Smith | Name of the user that made the last modification to a material economic of descriptive field.
| ChathamReferenceNumber | CFDEMOCORP2011120510 | Unique reference number assigned to the transaction by Chatham upon loading.
| ClientReferenceNumber | 10101010AB | Reference number assigned to the transaction by the client.
| CounterpartyReferenceNumber | 10101010AB | Reference number assigned to the transaction by the dealer counterparty.
| LoanReferenceNumber | 10101010AB | Reference number of the underlying loan related to the transaction (if applicable).
| UniqueSwapIdentifier | 1030282338VM60872468 | Unique swap identifier assigned to trade by the relevant swap data repository as required by the applicable regulation.
| Portfolio1 | My Derivative Portfolio | Custom name used to group a set of transactions. Transactions must belong to at least one portfolio.
| Portfolio2 | My Derivative Portfolio | Optional custom name used to group a set of transactions.
| Portfolio3 | My Derivative Portfolio | Optional custom name used to group a set of transactions.
| ProductType | Swap | Type of financial instrument of which the transaction consists.
| ProductDescription | Sells CNY/Buys USD Forward | Description of financial instrument of which the transaction consists (typically more detailed than 'ProductType').
| StrikeRateDescription | 58.00 - 52.825 USD-INR | Description of the strike price(s) or strike rate(s) for the transaction generated by Chatham upon loading.
| IndexDescription | 3 mo. EUR-Euribor-Telerate     | Description of the underlying index or rate(s) for the transaction generated by Chatham upon loading.
| SpreadDescription | 300.00 bps | Description of the spread(s) applied to the index for the transaction generated by Chatham upon loading.
| Description | Hedge of anticipated cash flow | Custom description of the transaction.
| Alias | 2013-03 CNY 8.59mm Sells CNY/Buys USD Forward Natixis | Descriptive nickname for the transaction generated by Chatham upon loading.
| HedgedItem | Floating Rate Term Loan A | Description of the item being hedged. This field is particularly relevant if hedge accounting is being applied to the trade.
| NotionalCurrency | USD | Currency in which the 'NotionalAmountDescription' is reported.
| NotionalAmountDescription | 10,000,000.00 | Description of the notional amount(s) of the transaction generated by Chatham upon loading.
| HomeCurrency | USD | For multi-currency transactions, this is the currency specified as the "home currency" at the time of trade loading. The other currency is the "foreign currency". This field returns null for single-currency transactions.
| FXCurrency | GBP | For multi-currency transactions, the "home currency" is set at the time of trade loading. This is the other currency, the "foreign currency". This field returns null for single-currency transactions.
| ClientLegalEntityName | MSREF VII HEDGING, L.P. | Legal name of entity related to Chatham's client that is party to the transaction.
| ClientLegalEntityIdentifier | 549300K1JD1LCRNAET48 | Legal entity identifier assigned to the entity related to Chatham's client that is party to the transaction.
| CounterpartyLegalEntityName | Natixis | Legal name of the entity that is the counterparty to Chatham's client in the transaction (e.g., a dealer bank).
| CounterpartyLegalEntityIdentifier | 549300K1JD1LCRNAET48 | Legal entity identifier assigned to the entity that is the counterparty to Chatham's client in the transaction (e.g., a dealer bank).
| ClearingStatus | [Accepted, Not Submitted, Resubmitted, Submitted, Rejected] | The status of a trade submitted for clearing to the ClearingHouse where the client is represented by the ClientClearingMember. Returns null for uncleared trades.
| ClientClearingMember | The Trust Company Limited | The name of the legal entity acting as the client's clearing member in a trade submitted to the ClearingHouse for clearing. Returns null for uncleared trades.
| ClearingHouse | ASX Limited | The legal name of the clearinghouse to which the trade was submitted for clearing. Returns null for uncleared trades.
| TradeDateTime | 2011-12-20T00:00:00.0000000-05:00 | Date and time when the trade was executed. Time is specified as 00:00:00.000 if it was not input.
| PremiumCurrency | USD | Currency in which the 'PremiumAmount' is paid.
| PremiumAmount | -400000.00 | Premium amount paid or received by 'ClientLegalEntity'. Positive means 'ClientLegalEntity' receives / 'CounterpartyLegalEntity' pays the amount. Negative means the 'ClientLegalEntity' pays / 'CounterpartyLegalEntity receives the amount.
| PremiumPaymentDate | 2011-12-22T00:00:00.0000000-05:00 | Date the 'PremiumAmount' was due to be paid.
| SwaptionDirection | [Buys, Sells] | Indicates whether the client is buying or selling the swaption. Returns null for other products.
| OptionExpirationDateTime | 2015-12-15T00:00:00.0000000-05:00 | For swaptions, FX options, and FX collars, the date and time when the option expires. Returns null for all others.
| SettlementDate | 2015-12-15T00:00:00.0000000-05:00 | Date of exchange or settlement for FX spot and FX forwards. Date when an exercised option is settled for swaptions, FX options, and FX collars. Returns null for all others.
| ScheduleType | [Bullet, Amortizing, Accreting, Roller Coaster] | Characterization of how the notional varies for interest rate transactions. Returns null for all others.
| EffectiveDate | 2017-03-20T00:00:00.0000000-04:00 | The start date for the first calculation period for interest rate transactions. Returns null for all others.
| MaturityDate | 2017-03-20T00:00:00.0000000-04:00 | This fields populates for all product types. For interest rate transactions, the last day of the last calculation period (not necessarily the last payment date). Same as the 'SettlementDate' for FX spot and FX forwards. Same date as the 'OptionExpirationDateTime' for FX options and FX collars.
| FxSettlementMethod | [Deliverable, Non-Deliverable] | For FX trades, indicates whether the transaction will by settled by physical exchange of the currency amounts ("Deliverable") or cash settled against a fixng rate ("Non-Deliverbale"). Returns null for interest rate transactions.
| Leg1Direction | [Sells, Buys, Pays, Receives] | This fields populates for all product types. For cross-currency swaps, interest rate swaps, and swaptions, indicates whether the 'ClientLegalEntity' pays or receives the interest payments associated with Leg 1. For interest rate caps, floors, collars, FX options, and FX collars, indicates whether the 'ClientLegalEntity' has bought or sold the right to receive the contingent cash flows associated with Leg 1. For FX spot and FX forwards, indicates whether the 'ClientLegalEntity' sells or buys the foreign currency amount included in Leg 1.
| Leg1Currency | USD | This fields populates for all product types. For interest rate transactions, the currency denomination of the interest payments associated with Leg 1. For FX trades, the same as 'Leg1FxCurrency'.
| Leg1Type | [Cap, Floor, Fixed, Floating, Put, Call, Spot, Forward] | This fields populates for all product types. For cross-currency swaps, interest rate swaps, and swaptions, indicates whether interest payments are "Fixed" or "Floating" for Leg 1. For options (other than swaptions), indicates the type of option. Indicates "Spot" or "Forward" for FX spot and FX forwards respectively.
| Leg1FxOptionStyle | European | For FX options and FX collars, the option style of the option captured in Leg 1. Returns null for all others.
| Leg1StrikeRate | 0.0350250 | For options, the strike rate. For swaps, the fixed rate. Returns null of the strike rate or fixed rate varies over the term of the trade. For FX spot and FX forwards, the exchange rate.
| Leg1StrikeRateFirstPeriod | 0.0350250 | For interest rate trades, the cap/floor rate or fixed rate for the first calculation period for Leg 1. It is equal to 'Leg1StrikeRate' when 'Leg1StrikeRate' is not null. Returns null for FX trades.
| Leg1StrikeRateForThisPeriod | 0.0350250 | The fixed rate or cap/floor rate applicable to Leg 1 for the period corresponding to 'Leg1PaymentDateForThisPeriod'.
| Leg1StrikeRateLastPeriod | 0.0350250 | For interest rate trades, the cap/floor rate or fixed rate for the last (final) calculation period for Leg 1. It is equal to 'Leg1StrikeRate' when 'Leg1StrikeRate' is not null. Returns null for FX trades.
| Leg1StrikeRateAsOfReportStart | 0.0350250 | For interest rate trades, the cap/floor rate or fixed rate for the calculation period in which the 'ReportStartDate' falls for Leg 1. For FX spot and FX forwards, the exchange rate. It is equal to 'Leg1StrikeRate' when 'Leg1StrikeRate' is not null and the 'ReportStartDate' is between the 'EffectiveDate' and 'MaturityDate' (for interest rate transactions) or between the 'TradeDateTime' and 'MaturityDate' (for FX transactions).
| Leg1StrikeRateAsOfReportEnd | 0.0350250 | For interest rate trades, the cap/floor rate or fixed rate for the calculation period in which the 'ReportEndDate' falls for Leg 1. For FX spot and FX forwards, the exchange rate. It is equal to 'Leg1StrikeRate' when 'Leg1StrikeRate' is not null, the 'ReportEndDate' is after the 'MaturityDate', and the trade was not terminated ahead of the 'ReportEndDate'.
| Leg1IndexName | USD-PEN | Name of the interest rate index or currency pair underlying Leg 1 of the transaction.
| Leg1IndexReutersCode | JPY= | The reuters code for the underlying index applicable to Leg1 as specified in 'Leg1IndexName'.
| Leg1SpreadOverIndex | 0.0375000 | For interest rate transactions the spread applied to the index for the purpose of calcualting interest payments for Leg 1. Returns null for "Fixed" legs and for all other product types or if the spread varies over the term of the trade.
| Leg1SpreadOverIndexFirstPeriod | 0.0375000 | For interest rate transactions the spread applied to the index for the first calculation period for Leg 1. Returns null for "Fixed" legs and for all other product types. It is equal to 'Leg1SpreadOverIndex' when 'Leg1SpreadOverIndex' is not null. Returns null for FX trades.
| Leg1SpreadOverIndexForThisPeriod | 0.0375000 | The spread applied to Leg 1 for the period corresponding to 'Leg1PaymentDateForThisPeriod'.
| Leg1SpreadOverIndexLastPeriod | 0.0375000 | For interest rate transactions the spread applied to the index for the last (final) calculation period for Leg 1. Returns null for "Fixed" legs and for all other product types. It is equal to 'Leg1SpreadOverIndex' when 'Leg1SpreadOverIndex' is not null. Returns null for FX trades.
| Leg1SpreadOverIndexAsOfReportStart | 0.0375000 | For interest rate transactions the spread applied to the index for the calculation period in which the 'ReportStartDate' falls for Leg 1. Returns null for "Fixed" legs and for all other product types. It is equal to 'Leg1SpreadOverIndex' when 'Leg1SpreadOverIndex' is not null and the 'ReportStartDate' is between the 'EffectiveDate' and 'MaturityDate'. Returns null for FX trades.
| Leg1SpreadOverIndexAsOfReportEnd | 0.0375000 | For interest rate transactions the spread applied to the index for the calculation period in which the 'ReportStartDate' falls for Leg 1. Returns null for "Fixed" legs and for all other product types. It is equal to 'Leg1SpreadOverIndex' when 'Leg1SpreadOverIndex' is not null, the 'ReportEndDate' is between the 'EffectiveDate' and 'MaturityDate', and the trade was not terminated ahead of the 'ReportEndDate'. Returns null for FX trades.
| Leg1PaymentFrequency | Monthly | For interest rate transactions, the payment frequency of Leg 1.
| Leg1DayCountConvention | [30/360, 30E/360, Act/360, Act/365 Fixed, Act/Act] | Indicates the day count method used to determine the number of days between two payment periods, for leg 1 of the transaction
| Leg1PeriodEndBusinessDayConvention | [Unadjusted, Preceding, Following, Modified Following, Modified Preceding] | Specifies the contractual convention of adjusting dates determined in respect to period end date, if period end date falls on a non Business Day.
| Leg1PaymentBusinessDayConvention | [Unadjusted, Preceding, Following, Modified Following, Modified Preceding] | Specifies the contractual convention of adjusting dates determined in respect to a payment date, if payment date falls on a non Business Day.
| Leg1StartDateForThisPeriod | 2017-02-20T00:00:00.0000000-04:00 | The first day of this calculation period for Leg 1.
| Leg1EndDateForThisPeriod | 2017-03-20T00:00:00.0000000-04:00 | For interest rate transactions, the last day of this calculation period for Leg 1. 
| Leg1DaysInThisPeriod | 30 | The number of days from and including the 'Leg1PeriodStartDate' and the 'Leg1PeriodEndDate'.
| Leg1NotionalCurrency | GBP | This fields populates for all product types. The currency of the notional applicable to Leg 1.
| Leg1NotionalAmount | 100000.00 | This fields populates for all product types. The notional amount applicable to Leg 1, not including the impact of amortization. For FX trades, this is the same as the 'Leg1FxCurrencyAmount'.
| Leg1NotionalAmountForFirstPeriod | 100000.00 | For interest rate transactions the notional amount for the first calculation period for Leg 1. Returns null for FX trades.
| Leg1NotionalAmountForPreviousPeriod | 100000.00 | The notional amount applicable to Leg 1 for the 'Leg1PaymentDateForPreviousPeriod'. Returns null if 'Leg1PaymentDateForPreviousPeriod' is null.
| Leg1NotionalAmountForThisPeriod | 100000.00 | The notional amount applicable to Leg 1 for the 'Leg1PaymentDateForThisPeriod'.
| Leg1NotionalAmountForNextPeriod | 100000.00 | The notional amount applicable to Leg 1 for this calculation period. Returns null if 'Leg1PaymentDateForNextPeriod' is null.
| Leg1NotionalAmountForLastPeriod | 100000.00 | For interest rate transactions the notional amount for the last (final) calculation period for Leg 1. Returns null for FX trades.
| Leg1NotionalAmountAsOfReportStart | 100000.00 | For interest rate transactions, the notional amount applicable to the period in which the 'ReportStartDate' falls for Leg 1; returns null if 'EffectiveDate' is after 'ReportStartDate'. For FX transactions, the 'Leg1FxAmount'; returns null if 'TradeDateTime' is after 'ReportStartDate'.
| Leg1NotionalAmountAsOfReportEnd | 100000.00 | For interest rate transactons, the notional amount applicable to the period in which the 'ReportEndDate' falls for Leg 1. For FX transactions, the 'Leg1FxAmount'. Returns null if 'ReportEndDate' is after the 'MaturityDate' or if a termination became effective during the current period.
| Leg1FxCurrency | GBP | For multi-currency transactions, the "home currency" is set at the time of trade loading. This is the other currency, the "foreign currency". This field returns null for single-currency transactions.
| Leg1FxCurrencyAmount | -176680.58 | For FX trades, the foreign currency amount to be exchanged at settlement or upon which the settlement will be based. Positive means 'ClientLegalEntity' receives / 'CounterpartyLegalEntity' pays the amount. Negative means the 'ClientLegalEntity' pays / 'CounterpartyLegalEntity receives the amount. For example, for a sold GBP call (where USD is the home currency) "-176680.58" would represent the INR call amount and is negative because it would be an amount paid by the 'ClientLegalEntity' if the option were to be exercised by the 'CounterpartyLegalEntity'. This fields returns null for interest rate transactions.
| Leg1HomeCurrency | USD | For multi-currency transactions, this is the currency specified as the "home currency" at the time of trade loading. The other currency is the "foreign currency". This field returns null for single-currency transactions.
| Leg1HomeCurrencyAmount | 282688.93 | For FX trades, the home currency amount to be exchanged at settlement or upon which the settlement will be based. Positive means 'ClientLegalEntity' receives / 'CounterpartyLegalEntity' pays the amount. Negative means the 'ClientLegalEntity' pays / 'CounterpartyLegalEntity receives the amount. For example, for a sold BRL call (where USD is the home currency) "282688.93" would represent the USD put amount and is positive because it would be an amount received by the 'ClientLegalEntity' if the option were to be exercised by the 'CounterpartyLegalEntity'. This fields returns null for interest rate transactions.
| Leg1FxFixingDate | 2017-03-20T00:00:00.0000000-04:00 | For non-deliverable FX trades, the date on which the settlement rate is determined. This field returns null for all other transactions.
| Leg1FxSettlementRate | 2.3515 | The FX rate used to determine the settlement amount of a non-deliverable FX trade. This field returns null for all others.
| Leg1FxSettlementAmount | 3367816.23 | The net amount paid or received by a party at on the settlement date of a non-deliverable FX trade. Positive means 'ClientLegalEntity' receives / 'CounterpartyLegalEntity' pays the amount. Negative means the 'ClientLegalEntity' pays / 'CounterpartyLegalEntity receives the amount. This field returns null for all others.
| Leg2Direction | [Sells, Buys, Pays, Receives] | For cross-currency swaps, interest rate swaps, and swaptions, indicates whether the 'ClientLegalEntity' pays or receives the interest payments associated with Leg 2. For interest rate collars and FX collars, indicates whether the 'ClientLegalEntity' has bought or sold the right to receive the contingent cash flows associated with Leg 2. Interest rate caps, floors, FX spot, FX forwards, and FX options do not have a Leg 2.
| Leg2Currency | GBP | For cross-currency swaps, interest rate swaps, swaptions, and collars, the currency denomination of the interest payments associated with Leg 2. For FX collars, the same as 'Leg2FxCurrency. Returns null for all others.
| Leg2Type | [Cap, Floor, Fixed, Floating, Put, Call, Spot, Forward] | For cross-currency swaps, interest rate swaps, and swaptions, indicates whether interest payments are "Fixed" or "Floating" for Leg 1. For interest rate collars and FX collars, indicates the type of option. Returns null for all others.
| Leg2FxOptionStyle | European | The specific type of FX option used for leg 1 of the transaction.
| Leg2StrikeRate | 1.3437 | For interest rate transactions, the fixed rate or cap/floor rate (if applicable) for Leg 2. Returns null if there is no Leg 2.
| Leg2StrikeRateFirstPeriod | 1.3437 | For interest rate trades, the cap/floor rate or fixed rate for the first calculation period for Leg 2 (if applicable). It is equal to Leg2StrikeRate when Leg2StrikeRate is not null. Returns null if there is no Leg 2.
| Leg1StrikeRateForThisPeriod | 1.3437 | The fixed rate or cap/floor rate applicable to Leg 2 for the period corresponding to 'Leg2PaymentDateForThisPeriod'.
| Leg2StrikeRateLastPeriod | 1.3437 | For interest rate trades, the cap/floor rate or fixed rate for the last (final) calculation period for Leg 2 (if applicable). It is equal to Leg2StrikeRate when Leg2StrikeRate is not null. Returns null if there is no Leg 2.
| Leg2StrikeRateAsOfReportStart | 1.3437 | The strike rate, cap/floor rate, or fixed rate for the calculation period in which the ReportStartDate falls for Leg 2 (if applicable). It is equal to 'Leg2StrikeRate' when 'Leg2StrikeRate' is not null and the 'ReportStartDate' is between the 'EffectiveDate' and 'MaturityDate' (for interest rate transactions) or the 'TradeDateTime' and 'MaturityDate' (for FX transactions). Returns null if there is no Leg 2.
| Leg2StrikeRateAsOfReportEnd | 1.3437 | The cap/floor rate, strike rate, or fixed rate for the calculation period in which the ReportEndDate falls for Leg 2 (if applicable). Returns null if the 'ReportEndDate' is after the 'MaturityDate' or 'TerminationEffectiveDate'. Returns null if there is no Leg 2.
| Leg2IndexName | 3 mo. USD-LIBOR-BBA | Name of the interest rate index or currency pair underlying Leg 1 of the transaction.
| Leg2IndexReutersCode | USD3MFSR= | The reuters code for the underlying index applicable to Leg1 as specified in 'Leg1IndexName'.
| Leg2SpreadOverIndex | 0.0250000 | The spread to the index being used for leg 2 of the transaction (should return blank if leg is fixed).
| Leg2SpreadOverIndexFirstPeriod | 0.0250000 | For interest rate transactions the spread applied to the index for the first calculation period for Leg 2. Returns null for "Fixed" legs and for all other product types. It is equal to 'Leg2SpreadOverIndex' when 'Leg2SpreadOverIndex' is not null. Returns null for FX trades.
| Leg2SpreadOverIndexForThisPeriod | 0.0250000 | The spread applied to Leg 2 for the period corresponding to 'Leg2PaymentDateForThisPeriod'.
| Leg2SpreadOverIndexLastPeriod | 0.0250000 | For interest rate transactions the spread applied to the index for the last (final) calculation period for Leg 2. Returns null for "Fixed" legs and for all other product types. It is equal to 'Leg12preadOverIndex' when 'Leg2SpreadOverIndex' is not null. Returns null for FX trades.
| Leg2SpreadOverIndexAsOfReportStart | 0.0250000 | For interest rate transactions the spread applied to the index for the calculation period in which the 'ReportStartDate' falls for Leg 2. Returns null for "Fixed" legs and for all other product types. It is equal to 'Leg2SpreadOverIndex' when 'Leg2SpreadOverIndex' is not null and the 'ReportStartDate' is between the 'EffectiveDate' and 'MaturityDate'. Returns null for FX trades.
| Leg2SpreadOverIndexAsOfReportEnd | 0.0250000 | For interest rate transactions the spread applied to the index for the calculation period in which the 'ReportStartDate' falls for Leg 2. Returns null for "Fixed" legs and for all other product types. It is equal to 'Leg2SpreadOverIndex' when 'Leg2SpreadOverIndex' is not null, the 'ReportEndDate' is prior to the 'MaturityDate', and the trade was not terminated ahead of the 'ReportEndDate'. Returns null for FX trades.
| Leg2PaymentFrequency | Semi-annually | For cross-currency swaps, interest rate swaps, swaptions and collars, the payment frequency of Leg 2.
| Leg2DayCountConvention | [30/360, 30E/360, Act/360, Act/365 Fixed, Act/Act] | Indicates the day count method used to determine the number of days between two payment periods, for leg 2 of the transaction
| Leg2PeriodEndBusinessDayConvention | [Unadjusted, Preceding, Following, Modified Following, Modified Preceding] | Specifies the contractual convention of adjusting dates determined in respect to period end date, if period end date falls on a non business day.
| Leg2PaymentBusinessDayConvention | [Unadjusted, Preceding, Following, Modified Following, Modified Preceding] | Specifies the contractual convention of adjusting dates determined in respect to a payment date, if payment date falls on a non business day.
| Leg2StartDateForThisPeriod | 2017-02-20T00:00:00.0000000-04:00 | The first day of this calculation period for Leg 2.
| Leg2EndDateForThisPeriod | 2017-03-20T00:00:00.0000000-04:00 | For interest rate transactions, the last day of this calculation period for Leg 2. 
| Leg2DaysInThisPeriod | 30 | The number of days from and including the 'Leg2PeriodStartDate' and the 'Leg2PeriodEndDate'.
| Leg2NotionalCurrency | GBP | The currency of the notional applicable to Leg 2.
| Leg2NotionalAmount | 160000.00 | The notional amount applicable to Leg 1. For FX collars this is the same as the 'Leg2FxCurrencyAmount'.
| Leg2NotionalAmountForFirstPeriod | 160000.00 | For interest rate transactions the notional amount for the first calculation period for Leg 2. Returns null for FX trades.
| Leg2NotionalAmountForPreviousPeriod | 160000.00 | The notional amount applicable to Leg 2 for the 'Leg2PaymentDateForPreviousPeriod'. Returns null if 'Leg2PaymentDateForPreviousPeriod' is null.
| Leg2NotionalAmountForThisPeriod | 160000.00 | The notional amount applicable to Leg 2 for the 'Leg2PaymentDateForThisPeriod'.
| Leg2NotionalAmountForNextPeriod | 160000.00 | The notional amount applicable to Leg 2 for this calculation period. Returns null if 'Leg2PaymentDateForNextPeriod' is null.
| Leg2NotionalAmountForLastPeriod | 160000.00 | For interest rate transactions the notional amount for the last (final) calculation period for Leg 2. Returns null for FX trades.
| Leg2NotionalAmountAsOfReportStart | 160000.00 | For interest rate transactions, the notional amount applicable to the period in which the 'ReportStartDate' falls for Leg 2; returns null if 'EffectiveDate' is after 'ReportStartDate'. For FX Collars, the 'Leg2FxAmount'; returns null if 'TradeDateTime' is after 'ReportStartDate'. Returns null if there is no Leg 2.
| Leg2NotionalAmountAsOfReportEnd | 160000.00 | For interest rate transactons, the notional amount applicable to the period in which the 'ReportEndDate' falls for Leg 2. For FX Collars, the 'Leg2FxAmount'. Returns null if 'ReportEndDate' is after the 'MaturityDate' or if a termination became effective during the current period. Returns null if there is no Leg 2.
| Leg2FxCurrency | GBP | For multi-currency transactions, the "home currency" is set at the time of trade loading. This is the other currency, the "foreign currency". This field returns null for single-currency transactions.
| Leg2FxCurrencyAmount | -176680.58 | For FX trades, the foreign currency amount to be exchanged at settlement or upon which the settlement will be based. Positive means 'ClientLegalEntity' receives / 'CounterpartyLegalEntity' pays the amount. Negative means the 'ClientLegalEntity' pays / 'CounterpartyLegalEntity receives the amount. For example, for a sold GBP call (where USD is the home currency) "-176680.58" would represent the INR call amount and is negative because it would be an amount paid by the 'ClientLegalEntity' if the option were to be exercised by the 'CounterpartyLegalEntity'. This fields returns null for interest rate transactions.
| Leg2HomeCurrency | USD | For multi-currency transactions, this is the currency specified as the "home currency" at the time of trade loading. The other currency is the "foreign currency". This field returns null for single-currency transactions.
| Leg2HomeCurrencyAmount | 282688.93 | For FX trades, the home currency amount to be exchanged at settlement or upon which the settlement will be based. Positive means 'ClientLegalEntity' receives / 'CounterpartyLegalEntity' pays the amount. Negative means the 'ClientLegalEntity' pays / 'CounterpartyLegalEntity receives the amount. For example, for a sold BRL call (where USD is the home currency) "282688.93" would represent the USD put amount and is positive because it would be an amount received by the 'ClientLegalEntity' if the option were to be exercised by the 'CounterpartyLegalEntity'. This fields returns null for interest rate transactions.
| Leg2FxFixingDate | 2017-03-20T00:00:00.0000000-04:00 | For non-deliverable FX trades, the date on which the settlement rate is determined. This field returns null for all other transactions.
| Leg2FxSettlementRate | 2.3515 | The FX rate used to determine the settlement amount of a non-deliverable FX trade. This field returns null for all others.
| Leg2FxSettlementAmount | 3367816.23 | The net amount paid or received by a party at on the settlement date of a non-deliverable FX trade. Positive means 'ClientLegalEntity' receives / 'CounterpartyLegalEntity' pays the amount. Negative means the 'ClientLegalEntity' pays / 'CounterpartyLegalEntity receives the amount. This field returns null for all others.
| Leg1CurrentPeriodNotionalCurrency | EUR | The currency of the notional amount applicable to the period in which the 'ReportEndDate' falls for Leg 1. Returns null if 'ReportEndDate' is after the 'MaturityDate' or if a termination became effective during the current period.
| Leg1IndexFixingDateForPaymentFollowingReportEnd | 2017-03-18T00:00:00.0000000-04:00 | The date on which the index rate is determined for the period in which the 'ReportEndDate' falls for Leg 1. Returns null if Leg 1 is a fixed leg or if 'ReportEndDate' is after the 'MaturityDate', or if a termination became effective during the current period. Returns null for FX transactions.
| Leg1IndexFixingDateForThisPeriod | 2017-03-18T00:00:00.0000000-04:00 | The date on which the index rate for Leg 1 is determined for the period corresponding to 'Leg1PaymentDateForThisPeriod'.
| Leg1IndexResetDateForPaymentFollowingReportEnd | 2017-03-20T00:00:00.0000000-04:00 | The reset date on which the rate fixing date is based for the period in which the 'ReportEndDate' falls for Leg 1. Returns null if Leg 1 is a fixed leg or if 'ReportEndDate' is after the 'MaturityDate', or if a termination became effective during the current period. Returns null for FX transactions.
| Leg1IndexResetDateForThisPeriod | 2017-03-20T00:00:00.0000000-04:00 | The reset date on which the rate fixing date for Leg 1 is based for the period corresponding to 'Leg1PaymentDateForThisPeriod'.
| Leg1IndexRateForPaymentFollowingReportEnd | 0.0016800 | The index rate as determined on the fixing date for the period in which the 'ReportEndDate' falls for Leg 1. Returns null if Leg 1 is a fixed leg or if 'ReportEndDate' is after the 'MaturityDate', or if a termination became effective during the current period. Returns null for FX transactions.
| Leg1IndexRateForThisPeriod | 0.00155 | The index rate for Leg 1 as determined on the 'Leg1IndexFixingDateForThisPeriod'.
| Leg1IndexRateForReportEnd | 0.00175 | The index rate for Leg 1 as determined on the 'ValuationDateTimeForReportEnd'.
| Leg1CurrentPeriodAllInRate | 0.0116800 | The sum of the index rate and spread for the period in which the 'ReportEndDate' falls for Leg 1. Returns null if Leg 1 is a fixed leg or if 'ReportEndDate' is after the 'MaturityDate', or if a termination became effective during the current period. Returns null for FX transactions.
| Leg1CurrentPeriodStartDate | 2017-03-20T00:00:00.0000000-04:00 | The first day of the calculation period in which the 'ReportEndDate' falls for Leg 1. Returns null if 'ReportEndDate' is after the 'MaturityDate' or if a termination became effective during the current period. Returns null for FX transactions.
| Leg1CurrentPeriodEndDate | 2017-03-20T00:00:00.0000000-04:00 | For interest rate transactions, the last day of the calculation period in which the 'ReportEndDate' falls for Leg 1. For FX options and FX collars, the same date as the 'OptionExpirationDateTime'. Returns null if 'ReportEndDate' is after the 'MaturityDate' or if a termination became effective during the current period.
| Leg1PaymentAmountForThisPeriod | -100000.00 | The gross amount due to be paid or received on the 'PaymentDate' with respect to Leg 1. A negative amount means the 'ClientLegalEntity' pays the amount, positive means the 'ClientLegalEntity' receives the amount.
| Leg1PaymentDatePrecedingReportEnd | 2017-02-20T00:00:00.0000000-04:00 | For interest rate transactions, the payment date related to the calculation period prior to the one in which the 'ReportEndDate' falls for Leg 1. Returns null for FX transactions.
| Leg1PaymentDateFollowingReportEnd | 2017-03-20T00:00:00.0000000-04:00 | For interest rate transactions, the payment date related to the calculation period in which the 'ReportEndDate' falls for Leg 1. For FX transactions, the 'SettlementDate'. Returns null if 'ReportEndDate' is after the 'MaturityDate' or if a termination became effective during the current period.
| Leg2CurrentPeriodNotionalCurrency | USD | The currency of the notional amount applicable to the period in which the 'ReportEndDate' falls for Leg 2. Returns null if 'ReportEndDate' is after the 'MaturityDate' or if a termination became effective during the current period. Returns null for transactions with no Leg 2.
| Leg2IndexFixingDateForPaymentFollowingReportEnd | 2017-03-18T00:00:00.0000000-04:00 | The date on which the index rate is determined for the period in which the 'ReportEndDate' falls for Leg 2. Returns null if Leg 2 is a fixed leg or if 'ReportEndDate' is after the 'MaturityDate', or if a termination became effective during the current period. Returns null for FX transactions and transactions with no Leg 2.
| Leg2IndexFixingDateForThisPeriod | 2017-03-18T00:00:00.0000000-04:00 | The date on which the index rate for Leg 2 is determined for the period corresponding to 'Leg2PaymentDateForThisPeriod'.
| Leg2IndexResetDateForPaymentFollowingReportEnd | 2017-03-20T00:00:00.0000000-04:00 | The reset date on which the rate fixing date is based for the period in which the 'ReportEndDate' falls for Leg 2. Returns null if Leg 2 is a fixed leg or if 'ReportEndDate' is after the 'MaturityDate', or if a termination became effective during the current period. Returns null for FX transactions and transactions with no Leg 2.
| Leg2IndexResetDateForThisPeriod | 2017-03-20T00:00:00.0000000-04:00 | The reset date on which the rate fixing date for Leg 2 is based for the period corresponding to 'Leg2PaymentDateForThisPeriod'.
| Leg2IndexRateForPaymentFollowingReportEnd | 0.0058875 | The index rate as determined on the fixing date for the period in which the 'ReportEndDate' falls for Leg 2. Returns null if Leg 2 is a fixed leg or if 'ReportEndDate' is after the 'MaturityDate', or if a termination became effective during the current period. Returns null for FX transactions and transactions with no Leg 2.
| Leg1IndexRateForThisPeriod | 0.00575 | The index rate for Leg 2 as determined on the 'Leg2IndexFixingDateForThisPeriod'.
| Leg2IndexRateForReportEnd | 0.0063175 | The index rate for Leg 2 as determined on the 'ValuationDateTimeForReportEnd'.
| Leg2CurrentPeriodSpreadOverIndex | 0.0145000 | The spread applied to the index rate for the period in which the 'ReportEndDate' falls for Leg 2. Returns null if Leg 2 is a fixed leg or if 'ReportEndDate' is after the 'MaturityDate', or if a termination became effective during the current period. Returns null for FX transactions and transactions with no Leg 2.
| Leg2CurrentPeriodAllInRate | 0.0203875 | The sum of the index rate and spread for the period in which the 'ReportEndDate' falls for Leg 2. Returns null if Leg 2 is a fixed leg or if 'ReportEndDate' is after the 'MaturityDate', or if a termination became effective during the current period. Returns null for FX transactions and transactions with no Leg 2.
| Leg2CurrentPeriodStartDate | 2017-03-20T00:00:00.0000000-04:00 | The first day of the calculation period in which the 'ReportEndDate' falls for Leg 2. Returns null if 'ReportEndDate' is after the 'MaturityDate' or if a termination became effective during the current period. Returns null for FX transactions and transactions with no Leg 2.
| Leg2CurrentPeriodEndDate | 2017-03-20T00:00:00.0000000-04:00 | For interest rate transactions, the last day of the calculation period in which the 'ReportEndDate' falls for Leg 2. For FX collars, the same date as the 'OptionExpirationDateTime'. Returns null if 'ReportEndDate' is after the 'MaturityDate', if a termination became effective during the current period, or transaction has no Leg 2.
| Leg2PaymentAmountForThisPeriod | 75000.00 | The gross amount due to be paid or received on the 'PaymentDate' with respect to Leg 2. A negative amount means the 'ClientLegalEntity' pays the amount, positive means the 'ClientLegalEntity' receives the amount.
| Leg2PaymentDatePrecedingReportEnd | 2017-02-20T00:00:00.0000000-04:00 | For interest rate transactions, the payment date related to the calculation period prior to the one in which the 'ReportEndDate' falls for Leg 2. Returns null for FX transactions.
| Leg2PaymentDateFollowingReportEnd | 2017-03-20T00:00:00.0000000-04:00 | For interest rate transactions, the payment date related to the calculation period in which the 'ReportEndDate' falls for Leg 2. For FX collars, the 'SettlementDate'. Returns null if 'ReportEndDate' is after the 'MaturityDate', if a termination became effective during the current period, or transaction has no Leg 2.
| PaymentDateForPreviousPeriod | 2017-02-20T00:00:00.0000000-04:00 | The previous payment date prior to the 'PaymentDateForThisPeriod'. Returns null if there is no previous period.
| PaymentDateForThisPeriod | 2017-03-20T00:00:00.0000000-04:00 | The date on which the Leg1PaymentAmount, Leg2PaymentAmount, or the NetPaymentAmount are due, if any.
| PaymentDateForNextPeriod | 2017-04-20T00:00:00.0000000-04:00 | The next payment date following the 'PaymentDateForThisPeriod'. Returns null if there is no next period.
| NetPaymentCurrency | USD | The currency in which the 'NetPaymentAmount' is denominated (if the two payments net). Returns null otherwise.
| NetPaymentAmountForThisPeriod | 25000.00 | The sum of 'Leg1PaymentAmount' and 'Leg2PaymentAmount' if both are in the same currency and due on the same 'PaymentDate'. Returns null otherwise.
| NumberOfPaymentDatesDuringTerm | 7 | The total number of payments in the schedule for interest rate transactions. Null for FX transactions.
| NumberInSquenceOfPaymentDateForThisPeriod | 2 | The number in chonological order corresponding to 'PaymentDateForThisPeriod'.
| FxVsHomeCurrencyPair | GBP-AUD | For multi-currency transcations, the currency pair composed from the foreign and home currencies (in the appropriate market convention). Returns null for single-currency transactions.
| FxVsHomeSpotRateForReportStart | 1.69605 | The spot rate for the 'FxVsHomeCurrencyPair' for the most recent market close prior to the 'ReportStartDate', quoted in the appropriate market convention. Returns null for single-currency transactions.
| FxVsHomeSpotRateForReportEnd | 1.7953 | The spot rate for the 'FxVsHomeCurrencyPair' for the most recent market close prior to the 'ReportEndDate', quoted in the appropriate market convention. Returns null for single-currency transactions.
| FxVsHomeSpotRateAsOfTradeDate | 1.6815 | The spot rate for the 'FxVsHomeCurrencyPair' as of the 'TradeDateTime', quoted in the appropriate market convention. Returns null for single-currency transactions.
| NotionalVsValuationCurrencyPair | GBP-AUD | The currency pair composed from the notional and valuation currencies (in the appropriate market convention).
| NotionalVsValuationSpotRateForReportStart | 1.69605 | The spot rate for the 'NotionalVsValuationCurrencyPair' for the most recent market close prior to the 'ReportStartDate', quoted in the appropriate market convention.
| NotionalVsValuationSpotRateForReportEnd | 1.7953 | The spot rate for the 'NotionalVsValuationCurrencyPair' for the most recent market close prior to the 'ReportEndDate', quoted in the appropriate market convention.
| NotionalVsValuationSpotRateAsOfTradeDate | 1.6815 | The spot rate for the 'NotionalVsValuationCurrencyPair' as of the 'TradeDateTime', quoted in the appropriate market convention.
| NotionalVsValuationSpotRateAsOfPaymentDateForThisPeriod | 1.6885 | The spot rate for the 'NotionalVsValuationCurrencyPair' as of the 'PaymentDateForThisPeriod', quoted in the appropriate market convention.
| AccruedInterestForReportEnd | -36169.97 | For interest rate transactions, the amount of interest accrued up through the 'ReportEndValuationDateTime'. Returns 0 for FX transactions.
| ReportingCurrency | TBD | The currency specified for this report in which transaction valuations and valuation-related fields are reported (for this report alone). The 'ReportingCurrency' overrides the 'ValuationCurrency'.
| AccruedInterestForReportStart | -36169.97 | For interest rate transactions, the amount of interest accrued up through the 'ReportStartValuationDateTime'. Returns 0 for FX transactions.
| CleanPriceForReportEnd | -889360.8 | The termination value less the accrued interest as of the 'ReportEndValuationDateTime'.
| CleanPriceForReportStart | -889360.8 | The termination value less the accrued interest as of the 'ReportStartValuationDateTime'.
| CreditValuationAdjustmentForReportEnd | NULL | The adjustment made to the termination value as of the 'ReportEndValuationDateTime' to account for the potential non-performance by the 'ClientLegalEntity'. This number is always equal to or greater than 0.
| CreditValuationAdjustmentForReportStart | 382274.44 | The adjustment made to the termination value as of the 'ReportStartValuationDateTime' to account for the potential non-performance by the 'ClientLegalEntity'. This number is always equal to or greater than 0.
| DebitValuationAdjustmentForReportEnd | NULL | The adjustment made to the termination value as of the 'ReportEndValuationDateTime' to account for the potential non-performance by the 'CounterpartyLegalEntity'. This number is always equal to or less than 0.
| DebitValuationAdjustmentForReportStart | -66532.57 | The adjustment made to the termination value as of the 'ReportStartValuationDateTime' to account for the potential non-performance by the 'CounterpartyLegalEntity'. This number is always equal to or less than 0.
| DeltaForReportEnd | NULL | For FX options and FX collars, the "delta" expressed as a fraction of the notional as of the 'ReportEndValuationDateTime', roughly equivalent to the likelihood of exercise. Returns null for non-option products.
| DeltaForReportStart | 0.2449 | For FX options and FX collars, the "delta" expressed as a fraction of the notional as of the 'ReportStartValuationDateTime', roughly equivalent to the likelihood of exercise. Returns null for non-option products.
| Dv01ForReportEnd | 20378.93 | For interest rate transactions, the change in the termination value that would result from a 1 basis point change in the key rate as of the 'ReportEndValuationDateTime'. Return null for FX trades.
| Dv01ForReportStart | 20378.93 | For interest rate transactions, the change in the termination value that would result from a 1 basis point change in the key rate as of the 'ReportStartValuationDateTime'. Return null for FX trades.
| FairValueForReportEnd | NULL | The sum of the termination value and the net credit adjustment as of the 'ReportEndValuationDateTime'.
| FairValueForReportStart | -14358356.34 | The sum of the termination value and the net credit adjustment as of the 'ReportStartValuationDateTime'.
| FxOptionDiscountFactorCurrency | USD | For FX transactions, the currency with respect to which the discount factor relates. Returns null for interest rate transactions.
| FxOptionDiscountFactorForReportEnd | 0 | For FX transactions, the currency with respect to which the discount factor for the 'ReportEndValuationDateTime' relates. Returns null for interest rate transactions.
| FxOptionDiscountFactorForReportStart | 0.99985 | For FX transactions, the discount factor used to present value the future settlement to the 'ReportStartValuationDateTime'. Returns null for interest rate transactions.
| FxOptionImpliedVolatilityForReportEnd | NULL | For FX options, the annualized volatility of the key underlying rate implied by the market as of the 'ReportEndValuationDateTime'. Returns null for non-option products.
| FxOptionImpliedVolatilityForReportStart | 0.1294 | For FX options, the annualized volatility of the key underlying rate implied by the market as of the 'ReportStartValuationDateTime'. Returns null for non-option products.
| KeyRateForReportEnd | 0.0074022 | The value of the key underlying rate for an equivalent at-market transaction as of the 'ReportEndValuationDateTime'. For interest rate transactions, the key rate is the at-market swap rate for remaining term. For FX transactions, the key rate is the at-market forward rate for the settlement date.
| KeyRateForReportStart | 0.0071365 | The value of the key underlying rate for an equivalent at-market transaction as of the 'ReportStartValuationDateTime'. For interest rate transactions, the key rate is the at-market swap rate for remaining term. For FX transactions, the key rate is the at-market forward rate for the settlement date.
| NetCreditAdjustmentForReportEnd | NULL | The sum of the credit and debit valuation adjustments as of the 'ReportEndValuationDateTime'.
| NetCreditAdjustmentForReportStart | 315741.87 | The sum of the credit and debit valuation adjustments as of the 'ReportStartValuationDateTime'.
| TerminationValueAsOfTradeDate | -925530.77 | The total mark-to-market value of the transaction, excluding the impact of non-performance risk by either party, as of the 'ReportStartValuationDateTime'. For all valuation fields, a positive value indicates an asset to the 'ClientLegalEntity' and a liability to the 'CounterpartyLegalEntity' and vice versa.
| TerminationValueForReportEnd | -925530.77 | The total mark-to-market value of the transaction, excluding the impact of non-performance risk by either party, as of the 'ReportEndValuationDateTime'. For all valuation fields, a positive value indicates an asset to the 'ClientLegalEntity' and a liability to the 'CounterpartyLegalEntity' and vice versa.
| TerminationValueForReportStart | -925530.77 | The total mark-to-market value of the transaction, excluding the impact of non-performance risk by either party, as of the 'ReportStartValuationDateTime'. For all valuation fields, a positive value indicates an asset to the 'ClientLegalEntity' and a liability to the 'CounterpartyLegalEntity' and vice versa.
| ValuationCurrency | EUR | The currency in which the transaction was set to value upon trade loading.
| ValuationCurrencyForReportEnd | EUR | The currency in which the transaction valuation was originally calculated for the 'ReportEndValuationDateTime'.
| ValuationCurrencyForReportStart | EUR | The currency in which the transaction valuation was originally calculated for the 'ReportStartValuationDateTime'.
| ValuationDateTimeForReportEnd | 2017-03-20T00:00:00.0000000-04:00 | The most recent transaction valuation timestamp on or prior to the 'ReportEndDate'.
| ValuationDateTimeForReportStart | 2017-03-20T00:00:00.0000000-04:00 | The most recent transaction valuation timestamp on or prior to the 'ReportStartDate'.
| VegaForReportEnd | -51.7 | For option transactions, the "vega" expressed in units of the 'ReportingCurrency' as of the 'ReportEndValuationDateTime', equal to the change in value due to 1% change in volatility. Returns null for non-option products.
| VegaForReportStart | -204102.95 | For option transactions, the "vega" expressed in units of the 'ReportingCurrency' as of the 'ReportStartValuationDateTime', equal to the change in value due to 1% change in volatility. Returns null for non-option products.
| StatusAsOfReportCreation | [Active, Matured, Terminated] | The status of the transaction as of the 'ReportCreationDateTime'. "Active" indicates the transaction has not yet reached the end of its term. "Matured" means that the "MaturityDate" has passed and that the transaction ran its natural course. "Terminated" means that the transaction was closed out and settled AHEAD of the 'MaturityDate'; in other words, one or more scheduled payments were cancelled ahead of maturity, typically in exchange for payment of a 'TerminationPremiumAmount'.
| StatusAsOfReportStart | [Active, Matured, Terminated] | The status of the transaction as of the 'ReportStartDate'. "Active" indicates the transaction has not yet reached the end of its term. Returns null if 'TradeDateTime' is after 'ReportStartDate'.
| StatusAsOfReportEnd | [Active, Matured, Terminated] | The status of the transaction as of the 'ReportEndDate'. "Active" indicates the transaction has not yet reached the end of its term. "Matured" means that the "MaturityDate" has passed and that the transaction ran its natural course. "Terminated" means that the transaction was closed out and settled AHEAD of the 'MaturityDate'; in other words, one or more scheduled payments were cancelled ahead of maturity, typically in exchange for payment of a 'TerminationPremiumAmount'.
| CounterpartyCommissionFee | 100.00 | The fee of type "commission" charged by the counterparty. Note that the fee does not carry a corresponding currency code.
| PaymentDateAfterReportEnd | 2017-03-20T00:00:00.0000000-04:00 | Date when the next scheduled payment after the 'ReportEndDate' is due to occur. For FX trades, this is the same as the 'SettlementDate'. This field returns null if there is no further payments scheduled for the transaction.
| PaymentDateBeforeReportStart | 2017-03-20T00:00:00.0000000-04:00 | Date of the most recent scheduled payment before the 'ReportStartDate'. For FX trades, this is the same as the 'SettlementDate'. This field returns null if there were no payments scheduled before the 'ReportStartDate'.
| TerminationTradeDate | 2017-03-20T00:00:00.0000000-04:00 | If the transaction was terminated ahead of maturity, this is the date on which the economics of the termination were agreed to between the parties. Returns null if the transaction is "Active" or "Matured".
| TerminationEffectiveDate | 2017-03-20T00:00:00.0000000-04:00 | If the transaction was terminated ahead of maturity, this is the date on which the termination become effective, the date after which no further obligations exist between the parties. Typically this is the same as the 'TerminationPremiumPaymentDate', but it may be different. Returns null if the transaction is "Active" or "Matured".
| TerminationPremiumCurrency | USD | If the transaction was terminated ahead of maturity and that resulted in a 'TerminationPremiumAmount' being due, this is the currency denomination of the 'TerminationPremiumAmount'. Returns null if the transaction is "Active" or "Matured".
| TerminationPremiumAmount | -700000.00 | If the transaction was terminated ahead of maturity and the termination resulted in a new payment obligation becoming due (typically in exchange for the extinguishment of all future obligations originally scheduled), this is that payment obligation. Returns null if the transaction is "Active" or "Matured".
| TerminationPremiumPaymentDate | 2017-03-20T00:00:00.0000000-04:00 | If the transaction was terminated ahead of maturity and that resulted in a 'TerminationPremiumAmount' being due, this is the date on which the 'TerminationPremiumAmount' is due. Returns null if the transaction is "Active" or "Matured".
| UserDefinedField1Name | Fund | User defined field name.
| UserDefinedField1Value | Kennett Square Fund II | User defined field value.
| UserDefinedField2Name | Country | User defined field name.
| UserDefinedField2Value | France | User defined field value.
| UserDefinedField3Name | Region | User defined field name.
| UserDefinedField3Value | Europe | User defined field value.
| UserDefinedField4Name | Strategy | User defined field name.
| UserDefinedField4Value | Asset level hedge | User defined field value.
| UserDefinedField5Name | Office | User defined field name.
| UserDefinedField5Value | New York | User defined field value.
| UserDefinedField6Name | JV Partner | User defined field name.
| UserDefinedField6Value | Local Investor LLC | User defined field value.
| UserDefinedField7Name | JV Partner Ref Nbr | User defined field name.
| UserDefinedField7Value | AA005623 | User defined field value.
| UserDefinedField8Name | Exposure Category | User defined field name.
| UserDefinedField8Value | FX risk | User defined field value.
| UserDefinedField9Name | Priority | User defined field name.
| UserDefinedField9Value | High | User defined field value.
| UserDefinedField10Name | Projected Deal Multiple | User defined field name.
| UserDefinedField10Value | 2.5X | User defined field value.




