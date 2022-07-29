# JavaAPI

Java trading SDK, a wrapper SDK of FIX API, provides clients with a fully functioning programmable API into the FXCM FX trading platform. The API’s main features are streaming executable FX trading prices, the ability to open/close positions and entry orders as well as set/update/delete stops ands limits. The API Object model is based on the FIX specification for FX. It is scalable, light and robust and is compatible on any Java-compliant operating system.

## How to start:
1) A FXCM account. You can apply for a demo account [here](https://www.fxcm.com/uk/algorithmic-trading/api-trading/)
2) Download the [package at here](https://apiwiki.fxcorporate.com/api/java/trading_sdk.zip)
3) Documents are in the package at trading_sdk\fxcm-api\javadoc.
4) Sample code at trading_sdk\fxcm-api\src\QATest.java
5) How to run QATest example:  
To run the program, it needs to be passed as below arguments:  
(loginid) (loginpwd) (connection_name) (hostUrl) (test_command) 	  	

		loginid: 
		   	Your Trading station username
		loginpwd:
		   	Your Trading station password
		connection_name:
		   	"Demo" or "Real"  
		hostUrl: 
		  	http://www.fxcorporate.com/Hosts.jsp 
		test_command is one of the following:
     		LISTEN:    Just listen for message, do not do anything
		 	CMO:       createMarketOrder (previously quoted)
		 	SSLMO:     set Stop/Limit on an open position
		 	USLMO:     update Stop/Limit price on a positon 
		 	DSLMO:     delete Stop/Limit from a position
		 	CEO:       create entry order 
		 	SSLEO:     set Stop/Limit on an entry order
		 	USLEO:     update Stop/Limit on an entry order
		 	DSLEO:     remove Stop/Limit on an entry order
		 	DEO:       remove Entry Order
		 	CLOSEMO:   close positon
		 	UREO:      Update rate on an entry order
			MDH:	   Retrieve Marke data history
			RECONNECT: Reconnect the session

## How to login:

    private void setup(IGenericMessageListener aGenericListener, boolean aPrintStatus) {
        try {
		// step 1: get an instance of IGateway from the GatewayFactory
            if (mFxcmGateway == null) {
                mFxcmGateway = GatewayFactory.createGateway();
            }
            /*
                step 2: register a generic message listener with the gateway, this
                listener in particular gets all messages that are related to the trading
                platform Quote,OrderSingle,ExecutionReport, etc...
            */
            mFxcmGateway.registerGenericMessageListener(aGenericListener);
            mStatusListener = new DefaultStatusListener(aPrintStatus);
            mFxcmGateway.registerStatusMessageListener(mStatusListener);
            if (!mFxcmGateway.isConnected()) {
                System.out.println("client: login");
                FXCMLoginProperties properties = new FXCMLoginProperties(mUsername, mPassword, mStation, mServer, mConfigFile);
                /*
                    step 3: call login on the gateway, this method takes an instance of FXCMLoginProperties
                    which takes 4 parameters: username,password,terminal and server or path to a Hosts.xml
                    file which it uses for resolving servers. As soon as the login  method executes your listeners begin
                    receiving asynch messages from the FXCM servers.
                */
                mFxcmGateway.login(properties);
            }
            //after login you must retrieve your trading session status and get accounts to receive messages
            mFxcmGateway.requestTradingSessionStatus();
            mAccountMassID = mFxcmGateway.requestAccounts();
        } catch (Exception e) {
            e.printStackTrace();
        }
    }

## How to get the rollover:

With Java API you can get the current rollover for each symbol, it can be done with the functions getFXCMSymInterestBuy()and getFXCMSymInterestSell() from TradingSecurity Class,  for Long and Short positions.

	For example:
	getFXCMSymInterestBuy() = 0.12     you will get $0.12 for 10k
	getFXCMSymInterestSell() = -0.39    you will pay $0.39  for 10k

	the 10k in this example is the server default base unit size, it can be found with FXCMParamValue where FXCMParamName = “BASE_UNIT_SIZE”

## Real Case Study:
1. How to build Rsi signal and back testing using FXCM Java API. <a href="https://apiwiki.fxcorporate.com/api/StrategyRealCaseStudy/JavaAPI/FXCM_Java_API_Tutorial_RsiSignal_Strategy.zip" target="_blank"> click here</a>
2. Learn how to build and backtest CCI Oscillator strategy using Java API at <a href="https://apiwiki.fxcorporate.com/api/StrategyRealCaseStudy/JavaAPI/CCIOscillatorStrategy-2.zip">here</a>.
3. Lean how to build and back test Breakout strategy using Java API at <a href="https://apiwiki.fxcorporate.com/api/StrategyRealCaseStudy/JavaAPI/BreakOutStrategy_JavaAPI.zip">here</a>. 
4. Lean how to build and back test Range Stochastic Strategy using Java API at <a href="https://apiwiki.fxcorporate.com/api/StrategyRealCaseStudy/JavaAPI/RangeStochasticStrategy.zip">here</a>. 
5. Lean how to build and back test Mean Reversion Strategy using Java API at <a href="https://apiwiki.fxcorporate.com/api/StrategyRealCaseStudy/JavaAPI/MeanReversionStrategy.zip">here</a>. 

## Note:
o	This is for personal use and abides by our [EULA](https://www.fxcm.com/uk/forms/eula/)

o	For more information, you may contact us: api@fxcm.com

## Release Note:
o	build.number=260: Roll up of all previous builds, plus fixes for range entry order with Good Til Date semantics;

o	Our price streams are moving from http to https using TLSv1.2 since 6/16/2019, to increase security on our price servers. 
	Please make sure client side software is compatible with TLSv1.2.
	Clients use ForexConnect API, Java API will be affected.
	The error you will get: ‘Can't connect to price server.’
	if you have any questions, please reach out to api@fxcm.com.

## Disclaimer:

High Risk Investment Notice: 

The FXCM Group is a holding company of Forex Capital Markets Limited (FXCM LTD), FXCM EU LTD (FXCM EU), FXCM Australia Pty. Limited (FXCM AU), FXCM South Africa (PTY) Ltd (FXCM ZA), FXCM Markets Limited (FXCM Markets), and all affiliates of aforementioned firms, or other firms under the FXCM Group of companies [collectively “FXCM”]. The FXCM Group is headquartered at 20 Gresham Street, 4th Floor, London EC2V 7JE, United Kingdom. Read and understand the Terms and Conditions on the FXCM Group’s websites prior to taking further action.

FXCM LTD: CFDs are complex instruments and come with a high risk of losing money rapidly due to leverage. 69% of retail investor accounts lose money when trading CFDs with this provider. You should consider whether you understand how CFDs work and whether you can afford to take the high risk of losing your money. FXCM LTD is authorised and regulated in the UK by the Financial Conduct Authority. Registration number 217689. Registered in England and Wales with Companies House company number 04072877.

FXCM EU: CFDs are complex instruments and come with a high risk of losing money rapidly due to leverage. 77% of retail investor accounts lose money when trading CFDs with this provider. You should consider whether you understand how CFDs work and whether you can afford to take the high risk of losing your money. FXCM EU is a Cyprus Investment Firm (“CIF”) registered with the Cyprus Department of Registrar of Companies (HE 405643) and authorised and regulated by the Cyprus Securities and Exchange Commission (“CySEC”) under license number 392/20.

FXCM AU: By trading, you could sustain a total loss of your deposited funds. The products may not be suitable for all investors. Please ensure that you fully understand the risks involved. If you decide to trade products offered by FXCM AU, you must read and understand the Financial Services Guide, Product Disclosure Statement, and Terms of Business. FXCM AU is regulated by the Australian Securities and Investments Commission, AFSL 309763. FXCM AU ACN: 121934432. The information provided by FXCM AU is intended for residents of Australia and is not directed at any person in any country or jurisdiction where such distribution or use would be contrary to local law or regulation. Please read the full Terms and Conditions.

FXCM Markets: Losses can exceed deposited funds. FXCM Markets is incorporated in Bermuda as an operating subsidiary within the FXCM group and is not required to hold any financial services license or authorisation in Bermuda to offer its products and services.

Past Performance: Past Performance is not an indicator of future results.
