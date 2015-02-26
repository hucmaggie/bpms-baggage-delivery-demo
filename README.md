JBoss BPM Suite Baggage Delivery Demo
=====================================
A baggage delivery service using BPM. A business friendly demo using form modeler, bpm process,
decisions table web, spreadsheet, dsl and bam.  

There are two options available to you for using this demo; local and OpenShift.


Option 1 - Install on your machine
----------------------------------
1. [Download and unzip.](https://github.com/jbossdemocentral/bpms-baggage-delivery-demo/archive/master.zip)

2. Add products to installs directory. For example download and add BPMS installer jar into the installs directory.

3. Run 'init.sh' or 'init.bat' file. 'init.bat' must be run with Administrative privileges.

4. Start JBoss BPMS Server by running 'standalone.sh' or 'standalone.bat' in the <path-to-project>/target/jboss-eap-6.1/bin directory.

5. Login to [http://localhost:8080/business-central](http://localhost:8080/business-central)

    ```
     - login for admin and other roles (u:erics / p:bpmsuite1!)
    ```


Option 2 - Install with one click in xPaaS (bpmPaaS)
----------------------------------------------------
After clicking button, ensure `Gear` size is set to `medium`:
  
[![Click to install OpenShift](http://launch-shifter.rhcloud.com/launch/light/Install
bpmPaaS.svg)](https://openshift.redhat.com/app/console/application_type/custom?&cartridges[]=https://raw.githubusercontent.com/jbossdemocentral/cartridge-bpmPaaS-travel-agency-demo/master/metadata/manifest.yml&name=travelagency&gear_profile=medium&initial_git_url=)

Once installed you can use the JBoss BPM Suite logins: 

   * u:erics   p: bpmsuite  (admin)

   * u: alan   p: bpmsuite  (analyst)

   * u: daniel p: bpmsuite (developer)

   * u: ursla  p: bpmsuite (user)

   * u: mary   p: bpmsuite (manager)


Running the demo
----------------
Build the project then kick off the process. An initial form will show for first name, last name, 
flyer status {None, Bronze, Silver, Gold} - (side note, can't figure out how to order these), 
Country Code, Zip if in US.  

If in US, will pass in zip code to zip code web service. Only the following zip codes will return 
states. Any other zip will return Texas.

	  //Park Ridge, IL
		zipCodes.put("60068", "IL");
		
		//Honolulu, HI
		zipCodes.put("96801", "HI");
		
		//New York, NY
		zipCodes.put("10001", "NY");
		
		//Bethel, AK
		zipCodes.put("99559", "AK");

After zip code service is called, the state field on passenger is used in web decision table to 
determine the cost of shipping.  Next, a DSL is used to figure out a surcharge for AK and HI.  

If not in US, county code is looked up in spreadsheet decision table and sets shipping and surcharge.

Finally, DSL is used to apply a promotion of free shipping and surcharge if passenger is of status Gold. 
You are then shown the route the process took and the variables to confirm shipping and surcharges are correct.

See docs directory for included spreadsheet decision table and presentation with highlights.

TODO: mavenize web service sources in projects directory.


Supporting Articles
-------------------
None yet...


Released versions
-----------------
See the tagged releases for the following versions of the product:

- v1.0 - JBoss BPM Suite 6.0.3 and baggage delivery demo installed.
