##  OFX v1.0.2 Summary
The information contained herein is a summary of part of the Open File Exchange specification version 1.0.2.  This version of the specification has been superseded however it remains in use by many financial institutions.  You can download the full specification from the [official Open File Exchange standard website](http://www.ofx.net/downloads.html)

I am interested in responses with transactions for bank, credit and loan accounts.  This summary focus's on those parts of the specification and is not intended to be comprehensive.

The symbols at the end of item names describe the structure:

* \* means the item is required 0 or more times
* \? means the item is required 0 or once only
* \+ means the item is required 1 or more times
* no symbol means the item is required once only
* \| symbol means either/or for the items to the left and right of the symbol
* \(\) symbols mean that the items enclosed by parenthesis are grouped together
* , symbol means that another item follows

I have used italics and bold for the items that are summarised.

###Response Message Structure
Every message contains a series of header lines followed by a blank line.  I have not described them here.  OFX is the top level item that follows.

* **OFX** contains (SIGNONMSGSRQV1, SIGNUPMSGSRQV1?, BANKMSGSRQV1?, CREDITCARDMSGSRQV1?, INVSTMTMSGSRQV1?, INTERXFERMSGSRQV1?, WIREXFERMSGSRQV1?, BILLPAYMSGSRQV1?, EMAILMSGSRQV1?, SECLISTMSGSRQV1?, PROFMSGSRQV1?) | (_SIGNONMSGSRSV1_, SIGNUPMSGSRSV1?, _BANKMSGSRSV1?_, CREDITCARDMSGSRSV1?, INVSTMTMSGSRSV1?, INTERXFERMSGSRSV1?, WIREXFERMSGSRSV1?, BILLPAYMSGSRSV1?, EMAILMSGSRSV1?, SECLISTMSGSRSV1?, PROFMSGSRSV1?)

* **SIGNONMSGSRSV1** contains _SONRS_, PINCHTRNRS?, CHALLENGETRNRS?

* **SONRS** contains _STATUS_, _DTSERVER_, _USERKEY?_, _TSKEYEXPIRE?_, _LANGUAGE_, _DTPROFUP?_, _DTACCTUP?_, _FI?_, _SESSCOOKIE?_

* **STATUS** contains _CODE_, _SEVERITY_, _MESSAGE?_

* **CODE** is a numeric value: INTTYPE
* **SEVERITY** is a text value: STRTYPE
* **MESSAGE** is a text value: STRTYPE

* **DTSERVER** is a date and time value: DTTMTYPE

* **USERKEY** is a text value: STRTYPE

* **TSKEYEXPIRE** is a date and time value: DTTMTYPE

* **LANGUAGE** is a text value: STRTYPE

* **DTPROFUP** is a date and time value: DTTMTYPE

* **DTACCTUP** is a date and time value: DTTMTYPE

* **FI** contains _ORG_, _FID?_

* **ORG** is a text value: STRTYPE
* **FID** is a text value: STRTYPE

* **SESSCOOKIE** is a text value: STRTYPE

* **BANKMSGSRSV1** contains (_STMTTRNRS_ | STMTENDTRNRS | INTRATRNRS | RECINTRATRNRS | STPCHKTRNRS | BANKMAILTRNRS | BANKMAILSYNCRS | STPCHKSYNCRS | INTRASYNCRS | RECINTRASYNCRS)+

* **STMTTRNRS** contains _TRNUID_ , _STATUS_ , _CLTCOOKIE?_, _STMTRS?_

* **TRNUID** is a unique identifier: UUIDTYPE (up to 36 character hexadecimal)

* **STATUS** re: above

* **CLTCOOKIE** is a text value: STRTYPE

* **STMTRS** contains _CURDEF_, _BANKACCTFROM_, _BANKTRANLIST?_, _LEDGERBAL_, _AVAILBAL?_, _MKTGINFO?_

* **CURDEF** is a text value: STRTYPE

* **BANKACCTFROM** contains _BANKID_, _BRANCHID?_, _ACCTID_, _ACCTTYPE_, _ACCTKEY?_

* **BANKID** is an identifier: IDTYPE
* **BRANCHID** is an identifier: IDTYPE
* **ACCTID** is an identifier: IDTYPE
* **ACCTTYPE** is an identifier: IDTYPE
* **ACCTKEY** is an identifier: IDTYPE

* **BANKTRANLIST** contains _DTSTART_, _DTEND_, _STMTTRN*_

* **DTSTART** is a date and time value: DTTMTYPE

* **DTEND** is a date and time value: DTTMTYPE

* **STMTTRN** contains _TRNTYPE_, _DTPOSTED_, _DTUSER?_, _DTAVAIL?_, _TRNAMT_, _FITID_, (_CORRECTFITID_, _CORRECTACTION_)?, _SRVRTID?_, _CHECKNUM?_, _REFNUM?_, _SIC?_, _PAYEEID?_, (_NAME_ | _PAYEE_)?, (_BANKACCTTO_ | _CCACCTTO_)?, _MEMO?_, (_CURRENCY_ | _ORIGCURRENCY_)?

* **TRNTYPE** is a text value: STRTYPE

* **DTPOSTED** is a date and time value: DTTMTYPE

* **DTUSER** is a date and time value: DTTMTYPE

* **DTAVAIL** is a date and time value: DTTMTYPE

* **TRNAMT** is an amount value: AMTTYPE

* **FITID** is an identifier: IDTYPE

* **CORRECTFITID** is an identifier: IDTYPE

* **CORRECTACTION** is a text value: STRTYPE

* **SRVRTID** is a server identifier: SRVRIDTYPE

* **CHECKNUM** is an identifier: IDTYPE

* **REFNUM** is a text value: STRTYPE

* **SIC** is a numeric value: INTTYPE

* **PAYEEID** is a server identifier: SRVRIDTYPE

* **NAME** is a text value: STRTYPE

* **PAYEE** contains _NAME_, _ADDR1_, (_ADDR2_, _ADDR3?_)?, _CITY_, _STATE_, _POSTALCODE_, _COUNTRY?_, _PHONE_

* **NAME** re: above
* **ADDR1** is a text value: STRTYPE
* **ADDR2** is a text value: STRTYPE
* **ADDR3** is a text value: STRTYPE
* **CITY** is a text value: STRTYPE
* **STATE** is a text value: STRTYPE
* **POSTALCODE** is a text value: STRTYPE
* **COUNTRY** is a text value: STRTYPE
* **PHONE** is a text value: STRTYPE

* **BANKACCTTO** contains the same as _BANKACCTFROM_ above

* **CCACCTTO** contains _ACCTID_, _ACCTKEY?_

* **ACCTID** re: above
* **ACCTKEY** re: above

* **MEMO** is a text value: STRTYPE

* **CURRENCY** contains _CURRATE_, _CURSYM_

* **CURRATE** is a rate value: RATETYPE
* **CURSYM** is a text value: STRTYPE

* **ORIGCURRENCY** contains the same as _CURRENCY_ above

* **LEDGERBAL** contains _BALAMT_, _DTASOF_

* **BALAMT** is an amount value: AMTTYPE
* **DTASOF** is a date and time value: DTTMTYPE

* **AVAILBAL** contains the same as _LEDGERBAL_ above

* **MKTGINFO** is a text value: STRTYPE

* **INTTYPE** is an integer value
* **STRTYPE** is a character string value
* **DTTMTYPE** is a date and time pair value: local time of system that created the data
* **UUIDTYPE** is a universal identier value: up to 36 hexadecimal characters
* **IDTYPE** is a general purpose identifier value
* **AMTTYPE** is an amount value: may be signed; comma or period for decimal point
* **SRVRIDTYPE** is a value identifying the type of a server identifier
* **RATETYPE** is a rate, percentage value
