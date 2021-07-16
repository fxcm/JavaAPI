CFDs are complex instruments and come with a high risk of losing money rapidly due to leverage.

**70% of retail investor accounts lose money when trading CFDs with this provider.**

You should consider whether you understand how CFDs work and whether you can afford to take the high risk of losing your money.

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

Trading Forex/CFDs on margin carries a high level of risk and may not be suitable for all investors. The products are intended for retail, professional, and eligible counterparty clients. Retail clients who maintain account(s) with Forex Capital Markets Limited (“FXCM LTD”) could sustain a total loss of deposited funds but are not subject to subsequent payment obligations beyond the deposited funds but professional clients and eligible counterparty clients could sustain losses in excess of deposits. Clients who maintain account(s) with FXCM Australia Pty. Limited (“FXCM AU”), FXCM South Africa (PTY) Ltd (“FXCM ZA”) or FXCM Markets Limited (“FXCM Markets”) could sustain losses in excess of deposits. Prior to trading any products offered by [FXCM LTD](https://www.fxcm.com/uk/), inclusive of all EU branches, [FXCM AU](https://www.fxcm.com/au/), [FXCM ZA](https://www.fxcm.com/za/), any affiliates of aforementioned firms, or other firms within the FXCM group of companies [collectively the “FXCM Group”], carefully consider your financial situation and experience level. If you decide to trade products offered by FXCM AU (AFSL 309763), you must read and understand the [Financial Services Guide](https://docs.fxcorporate.com/financial-services-guide-au.pdf), [Product Disclosure Statement](https://www.fxcm.com/au/legal/product-disclosure-statements/), and [Terms of Business](https://docs.fxcorporate.com/tob_au_en.pdf). Our Forex/CFD prices are set by FXCM, are not made on an Exchange and are not governed under the Financial Advisory and Intermediary Services Act. The FXCM Group may provide general commentary, which is not intended as investment advice and must not be construed as such. Seek advice from a separate financial advisor. The FXCM Group assumes no liability for errors, inaccuracies or omissions; does not warrant the accuracy, completeness of information, text, graphics, links or other items contained within these materials. Read and understand the Terms and Conditions on the FXCM Group’s websites prior to taking further action. 
