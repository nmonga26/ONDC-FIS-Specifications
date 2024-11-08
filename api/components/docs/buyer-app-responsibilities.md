The buyer app is expected to take care of the following

### 2 Factor Authentication
Perform 2 factor authentication for all orders before confirming.  

One factor is sending otp to investor's email/mobile. Other factor can be anything other than this.  
1. For transaction in existing folio - use the email/mobile present in the folio  
2. For transaction in new folio - use the email/mobile added as communication details in the folio opening form  

The email/mobile used for this 2fa should be sent by BAP as part of the `/init` call.

### Verify contact email and mobile
Verify that the contact email address and mobile number given in new folio opening form, exists and investor has access to it.

### Clickwrap consent to terms and conditions
BPP sends the terms and conditions that the investor has to accept, in `CONSUMER_TNC` tag in scheme plan item. BAP should show these terms to the investor, and let him explicitly agree to those, before calling `/init`. BAP can either show a checkbox or a button to get the investor consent. BAP has to keep information related to the investor acceptance of these tncs like the time of acceptance, mode of acceptance, ip address from where it is accepted etc. (this is to provide details if the investor challenges his acceptance at a later point in time). As part of the protocol, `IP_ADDRESS` from where the investor accepted these TNCs should be sent by the BAP.
When it receives the `/init` call, BPP assumes that the investor clickwrap consent has been taken.

This is applicable for cancellation calls also in the same way as described for init calls.