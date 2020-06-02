Appendix A: f5 WAF Tester Administrator Guide
==============================================

To install on different platforms:
Ubuntu/Kali 

        .. code-block:: bash
        
                sudo apt-get install -y python-pip
Fedora

        .. code-block:: bash
        
                sudo dnf install -y python-pip

More information can be observed by clicking f5-waf-tester --help
usage: f5-waf-tester [-h] [-v] [-i] [-c CONFIG] [-t TESTS] [-r REPORT]

optional arguments:
  -h, --help            Show this help message and exit
  -v, --version         Show program's version number and exit
  -i, --init            Initialize Configuration. (default: False)
  -c CONFIG, --config CONFIG
                        Configuration File Path. (default:
                        /usr/local/lib/python2.7/dist-
                        packages/f5-waf-tester/config/config.json)
  -t TESTS, --tests TESTS
                        Tests File Path. (default: /usr/local/lib/python2.7
                        /dist-
                        packages/f5-waf-tester/config/tests.json)
  -r REPORT, --report REPORT
                        Report File Save Path. (default: report.json)

When going through the configuration file prompts (./f5-waf-tester –init), there are more prompts that you can configure:

        Blocking Regular Expression Pattern [<br>Your support ID is: (?P<id>\d+)<br>]: 
                Specifies where to grab your support ID from the block page.  This should remain unchanged unless you have a customized block page.

	Number OF Threads [25]: 
	        Number of threads to open in parallel

	[Filters] Test IDs to include (Separated by ',') []: 
                You can specify test IDs to run if you do not want all 24 tests to execute. (See Appendix B for full matrix)

	[Filters] Test Systems to include (Separated by ',') []: 
                You can specify test systems to run if you do not want all of them to execute.  

                        Here are the possible systems that can be used:
                                All Systems
                                General Database
                                MongoDB
                                Unix/Linux
                                Microsoft Windows
                                Node.js
                                PHP

        [Filters] Test Attack Types to include (Separated by ',') []: 
	        Specify attack types to run if you do not want to run all.  
                
                The options are:
		        XSS

                        SQL Injection

                        NoSQL Injection

                        Command Execution

                        Path Traversal

                        Predictable Resource Location

                        HTTP Protocol Compliance

                        Detection Evasion

                        Insecure Deserialization

                        Information Leakage

                        JSON Parser Attack

                        XML Parser Attack

                        HTTP Parser Attack

                        HTTP Request Smuggling

                        Server Side Request Forgery


        [Filters] Test IDs to exclude (Separated by ',') []: 
                Exclude test IDs to be run.

        [Filters] Test Systems to exclude (Separated by ',') []: 
                Exclude test systems to be run.

        [Filters] Test Attack Types to exclude (Separated by ',') []:
                Exclude attack types to be run.

Here are the possible reasons that could cause the test ID to fail:
        ASM Policy is not in blocking mode

        Attack Signature is not in the ASM Policy

        Attack Signatures are not up to date

        Attack Signature disabled

        Attack Signature is in staging

        Parameter * is in staging

        URL * is in staging

        URL * Does not check signatures

        Header * Does not check signatures

        Evasion disabled

        Evasion technique is not in blocking mode
        
        Violation disabled