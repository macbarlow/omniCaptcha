# A-HLS omniCaptcha

## What is omniCaptcha?

omniCaptcha is a custom LWC developed to be used in a OmniScript that is hosted on a Experience Cloud page.   It allows you to leverage Google reCAPTCHA for that OmniScript.

This version leverages reCAPTCHA v2 checkbox.  More information about reCAPTCHA can be found at: https://www.google.com/recaptcha/about/
You will need to setup an account and add your FQDNs to receive your Site Key and Secret Key required to validate your page reCAPTCHA.  

![Image: images/recaptcha.png](/images/recaptcha.png)


## What is included in omniCaptcha?

### omniCaptcha LWC
-	omniCaptcha.html
-	omniCaptcha.js
-	omniCaptcha.js-meta.xml

### OmniStudio Integration Procedure
-	validate_captcha.json (Importable Datapack)

### Custom Head Markup for Experience Cloud site where this will be used
-	Markup.html

## Installation

1. Add the omniCaptcha LWC to your Org using the methods you typically use.  
2. Download and import the Integration Procedure

## Configuration

### Experience Cloud 

1. You need to navigate to the site settings->Security & Privacy page
- Set the Security Level to Relaxed
- Add two Trusted Sites as follows
  - Google – https://www.google.com
  - GStatic – https://www.gstatic.com

  ![Image: images/trusted_sites.png](/images/trusted_sites.png)

2. Still in settings navigate to Advanced and click the Edit Head Markup button. 
   - Add the content of the Markup.html file here and click save.  
   - Add your Site Key in this file where it says ENTER_SITE_KEY_HERE
3. Navigate to Org Settings->CSP Trusted Sites and add the following:
   - Google – https://www.google.com
   - GStatic – https://www.gstatic.com
4. Navigate to Org Settings->Remote Site Settings and add the following: 
   - Google – https://www.google.com    
   - GStatic – https://www.gstatic.com

### OmniStudio

### Integration Procedure

1. Open the validate_captcha Integration Procedure.
   - In the second HTTP action node open the REST OPTIONS and add your secret key from Google where it says ENTER_YOUR_SECRET_KEY_HERE
   - Save and Activate the IP
 ![Image: images/IP.png](/images/IP.png)


### OmniScript

1. Add the Custom LWC input to your OmniScript.  Select omniCaptcha
   - To enable Debug mode add a  Custom LWC Property of Debug = true
2. omniCaptcha will write to the JSON in your OS under the name of the Custom LWC component.  It will create isHuman as either true or false.  
3. To hide the next button on the step that includes omniCaptcha you need to set conditional view of all the nodes that follow.  

![Image: images/conditional_view.png](/images/conditional_view.png)
 
### For Guest access in Experience Cloud Site

1. Grant access to three apex classes
   - vlocity_ins.BusinessProcessController
   - vlocity_ins.BusinessProcessDisplayController
   - vlocity_ins.PlatformObjectMappings


![Image: images/apex.png](/images/apex.png)


2. Grant Read access for two objects
   - vlocity OmniScripts
   - vlocity OmniScript Compiled Definitions
     - Grant read access to 'Content' & 'Sequence' fields

![Image: images/objects.png](/images/objects.png)
![Image: images/Compiled.png](/images/Compiled.png)


Note:  
  - If the reCAPTCHA fails isHuman will be set to false.  
  - If it succeeds it will be true. 
  - Debug data is written to the console of the browser. 
