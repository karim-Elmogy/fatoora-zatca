<p align="center">
  <img src="https://login.zatca.gov.sa/com.sap.portal.resourcerepository/repo/zatca/img/ZATCA-logo.png" alt="ZATCA Logo">
</p>


# Fatoora Zatca

This package handle the phase 2 of the zakat and income authority in the saudi arabia, addition to it's based on native php so it can work on any system based on php or any framework like: (Laravel - Symfony - CodeIgniter - Yii - Zend Framework - CakePHP) 

### The package handle 3 environments:
- [x] test.
- [x] simulation.
- [x] production.

**Requirements**
* phpseclib/phpseclib:~3.0
* simplesoftwareio/simple-qrcode

## Installation
```bash
composer require elmogy/fatoora-zatca
```


**Configuration:**

```
 # Must add the service provider to config/app.php
 'providers' => [
    /*
    * Package Service Providers...
    */
    Bl\FatooraZatca\FatooraZatcaServiceProvider::class,
 ]
```

## Then publish the config file 👏

```
php artisan vendor:publish --tag=fatoora-zatca
```


## Assign the config from your.env
```
 ZATCA_ENVIRONMENT=local   # local|simulation|production
```


## Setting
```
First you must generate credentials to use in zatca authentication 
and here is the steps :  
1- fill all parameters in Setting object.
 $settings = new \Bl\FatooraZatca\Objects\Setting();
 2 - pass $settings to the static method ( generateZatcaSetting ) 
$result = \Bl\FatooraZatca\Zatca::generateZatcaSetting($settings);
 3 - save all $result object to database to use when sending xml invoices.
 Prepare
 $seller       
instance of \Bl\FatooraZatca\Objects\Seller::class
 $invoice    instance of \Bl\FatooraZatca\Objects\Invoice::class
 $client       
instance of \Bl\FatooraZatca\Objects\Client::class
 \Bl\FatooraZatca\Classes\InvoiceType 
(TAX_INVOICE|REFUND_INVOICE|CREDIT_NOTE)
 \Bl\FatooraZatca\Classes\PaymentType (CASH|CREDIT|BANK_ACCOUNT|
 BANK_CARD|MULTIPLE)
 B2B Invoice Tax
 $invoice = \Bl\FatooraZatca\Invoices\B2B::make($seller, $invoice, $client)->report();
 B2C Invoice Tax
 $invoice = \Bl\FatooraZatca\Invoices\B2C::make($seller, $invoice)->report();
 OR
 $invoice = \Bl\FatooraZatca\Invoices\B2C::make($seller, $invoice)->calculate();
```



## Access Response
```
 $invoice->getQr();                            # qr text in base64 format
 $invoice->getQrImage();                       # qr image in base64 format
 $invoice->getInvoiceHash();                   # the hash of the invoice
 $invoice->getClearedInvoice();                # the invoice in base64 format
 $invoice->getXmlInvoice();                    # the invoice in xml format
 $invoice->getReportingStatus();               # Status of clearance and reporting   
 $invoice->getValidationResultStatus();        # validation status of sent data
 $invoice->getValidationResults();             # all messages (info - warning - error)
 $invoice->getInfoMessages();                  # all info messages
 $invoice->getWarningMessages();               # all warning messages
 $invoice->getErrorMessages();                 # all error messages
 $invoice->getResult();                        # access all the previous data
       
```
