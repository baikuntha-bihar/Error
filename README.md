Issue 1: ATRN is saved as NULL

· Log Line: Successfully saved merchant payment order with ATRN is null and mid is 1000890
· Problem: The system creates the transaction record but does not save an ATRN in the database.
· Fix: In MerchantOrderPaymentDao.java, ensure the ATRN is generated or retrieved before saving the record so it is not null.

Issue 2: Mismatched ATRN sent to downstream

· Log Line: Initiating SBI INB payment request: PaymentINBRequest(atrn=NB890MI2158VMAFAPIQQ)
· Problem: The system tries to initiate the payment using an ATRN that the downstream payment service does not recognize (because it was never properly created or saved).
· Fix: In PaymentServicesClient.java (Line 86), ensure you are sending the exact ATRN that was successfully created and saved in the database.

Issue 3: Downstream Service Rejects the Request

· Log Line: ErrorDto(errorCode=3002, errorMessage=atrn is invalid. Reason: Transaction status or atrn is not valid.)
· Problem: The payment-paymentservice checked its database, couldn't find the ATRN NB890MI2158VMAFAPIQQ, or found it in the wrong status, and rejected the call.
· Fix: In PaymentServicesClient.java, add a step to first create/register the transaction in the payment-paymentservice to generate a valid ATRN. Only after that succeeds, call initiateSBIINBPayments with that valid ATRN.

Summary of Logs Issue: The logs show the transaction fails at the very last step (external API call) because the ATRN sent to the payment service is invalid. The root cause is in MerchantOrderPaymentDao.java (saving null ATRN) and PaymentServicesClient.java (using an invalid ATRN for the call).
