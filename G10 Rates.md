# Table of Contents

US	3

JP	8

AU	11

Rates Basics	16

Terms	17


<div style="page-break-after: always;"></div>

**understand fiscal spending in each market, how does the auction process works , what drives the basis (essentially who issues hard and soft currency, this abit hard need learn on the job).**

**be familiar with what drives price action within each market, what to look out for etc , diff from each country.**

**Understand more about repo market , hence how to model fair value of swap spread , RoW ASW swap spread = Swap - Bond, JP Asw = bond – swap**

**but js understand what is tradable and what drives price action is more impt**

**think can focus more on US and JP rates market , understand the plumbing and repo make sure u understand**

**Please get yourself equipped with how to build USD rates curve, bootstrapping, risk calculation method, different instruments used in IR market, curve strategies and economy movers. Carry/Roll etc to formulate your view on top of macro events etcetc**


<div style="page-break-after: always;"></div>


# US

Fiscal Spending: Every quarter have bond issuance plan.

1. Huge fiscal pressure, from primary dealer estimate, FY2026 (10/1/2025 – 9/30/2026) 1.95trn, FY2027 2.02trn, privately-held net marketable borrowing FY2026 2.04trn, FY2027 2.10trn. However, market understand US have huge fiscal deficit, so the marginal variable is, 2trn funding need will be bills or coupons, especially for 10y/20y/30y.
   1. If most funding needs by bills, money market, cash investors, repo market would take it, bill yields may cheaper than <span style="color:#ee0000">OIS/SOFR</span>, limited impact to long-end.
   2. If funding needs on coupons, long-end supply increase, term premium increase, auction concession would increase, curve would steepen (bear steepen)
2. For short, May 2026 quarterly refunding gave market a short relief: keep <span style="color:#ee0000">nominal coupon and FRN auction size</span> unchanged and expect future few quarter won’t increase coupon sizes. So, more pressure would on Treasury bills; cash balance and <span style="color:#ee0000">TGA management</span>.
So for mid-to-long term, large fiscal deficits remain a structural source of higher term premium and long-end supply risk.

While for short term, Treasury would adjust bill auction sizes and cash management to take funding need.

\*<span style="color:#ee0000">what</span> <span style="color:#ee0000">to track, which web</span>

Bond Auction: The issuance process is kicked off at the Treasury’s quarterly refunding meetings which announce the government’s forecasted financing needs, upcoming coupon auction sizes, and sets the auction schedule. Auction results provide useful information about demand of UST, we should focus on 1) high yield when-issued 2) bidder allocation 3) bid-to-cover ratio. Fed rollovers: should have no impact on the strength of an auction.

1. Treasury issuance process: TGA: Treasury’s cash balance; FRN: Floating Bond
   1. Quarterly refunding process: QRA allows Treasury to update the market on its financing needs, auction sizes &amp; schedule, any potential policy or issuance changes it is considering. (Advised by TBAC) – first week of Feb, May, Aug, Nov: 1) updated financing estimates on Mon 3pm ET; 2) refunding announcement &amp; issuance decisions on Wed 830am ET. **Important takeaway**: Treasury’s projected financing needs and issuance plans.
![image1.png](<G10 Rates_media/image1.png>)

   2. How Treasury auctions work: For coupon (notes, bonds, FRNs, TIPS) offering size, market should know from QRA, but bill auction sizes tend to be announced on Tue/Thu for settlement the following week.
(1) security, (2) offering amount, (3) auction date, (4) issue/settlement date, (5) maturity date, (6) interest payment dates, (7) max award and minimum bid amounts, (8) **how much is maturing from the Fed’s System Open Market Account (SOMA),** and (9) closing times for the non-competitive and competitive auctions

There are non-competitive and competitive bidding. Noncompetitive is done ahead of the competitive bidding auction.  FIMA/SOMA; SOMA count as add-on, and is not included in the offering amt.

Competitive is Dutch auction, take highest yield bid regardless of the rate they bid.

Net Long Position: investor has bought (or agreed to buy) more than it has sold (or agreed to sell) of a particular security

Conpons pay interest every 6 month, bills no coupon payment, the discount is considered interest.

   3. Products:
      1. Bills: Price = Fair Value (1-(discount rate x time)/360), 4-, 8-, 13-, 17-, 26-, and 52-week + CMBs.
      2. Notes: 2-10years, 6-month payment
      3. Bonds: 20-,30-
      4. TIPS: 5-, 10-, and 30-year, price and interest rate are also determined at auction, but the principal on TIPS goes up and down with inflation and deflation, CPI.
      5. FRNs: 2-, an index rate and a spread, index rate is 13-week bill
![image2.png](<G10 Rates_media/image2.png>)

![image3.png](<G10 Rates_media/image3.png>)

![image4.png](<G10 Rates_media/image4.png>)

![image5.png](<G10 Rates_media/image5.png>)

   4. Reopening: if a 7-year note, with an interest rate of 4% rolls down 2 years and a new issue 5-year note auction also results in a 4% interest rate, Treasury will announce that the auction results have prompted an unscheduled reopening of the 7-year note.
   5. Coupon rate = annual payment / face value; Current yield = annual payment / market value
   6. Analyze auction results: Comparing the results of previous auction for same term, 1) high yield relative to the when issued rate 2) the bidder allocations 3) the bid to cover ratio.
      1. High yield: Highest yield that was accepted, comparing with issued rate: 1) traded through, 2) tailed, 3) printed “on the screws” Trade through: Bond demand strong, Tailed: Weak demand, On the screwed: Neither
      2. Bidder Allocation: Determine from this data whether the demand was end investor demand or dealer demand. Primary dealer was bidder for themselves. High percentage of PD takedown is a negative signal. Direct bidder higher is a positive signal. Indirect often seen as a proxy for foreign accounts.
      3. Bid-to-cover: At face value, the higher the cover the better the auction, but not perfect as it includes dealer bids. But typically a bid-to-cover ratio that is higher than the average for prior auctions of the same tenor would imply it is a stronger auction while lower would indicate a weaker auction.
2. Markets dynamics: General historical relationship hard to find, but locally around auctions can find. (Price action with 10yT auctions)
3. Fed Rollovers: QE: buying UST; Rollovers: Holding and reinvesting UST; QT: redeeming or selling USTs. The more the Fed holds of USTs, the less the public will need to hold, putting downward pressure on rates.

![image6.png](<G10 Rates_media/image6.png>)

4. Treasury buybacks: Operation like QE, but the purchases are funded by Treasury cash balance or other Treasury debt issuance and not by the Fed creation of reserves.
   1. Buckets: &gt;2 yr maturities; &lt;2 yr CMB
   2. Amount: 30B every quarter maximum
   3. Security exclusions; per CUSIP
Repo market:

1. SOFR – based on Treasury repo rate, measuring UST as collateral’s financing cost.
2. Swap Spread: SOFR Swap rate – Treasury yield. Why would repo affect swap? **ASW Package: Buy Treasury + pay fixed SOFR swap + fund Treasury in repo.** (repo from funding need for UST). Carry = Treasury Yield – Swap Rate + SOFR – Repo; Fair Swap Spread = SOFR - Repo (Carry = SOFR - Repo – ASW = 0)
3. 4 kinds of repo condition:
   1. GC repo: General Collateral – general Treasury funding condition. If GC repo higher than SOFR, indicates that cash/balance sheet liquidity is tighter and treasury funding is more expensive.
   2. Specials: Specific Treasury is in demand. The bond is trading special in repo, which supports the ASW richness.
   3. Balance Sheet Pressure: Sometimes repo rate is not high, while dealer may don’t wanna have more treasury inventory due to balance sheet constraint.
   4. Fed facilities: ON RRP; SRF; reserves/QT/TGA
4. We can see swap spread as two leg: Treasury leg + Swap Leg:
![image7.png](<G10 Rates_media/image7.png>)

![image8.png](<G10 Rates_media/image8.png>)

![image9.png](<G10 Rates_media/image9.png>)


<div style="page-break-after: always;"></div>


# JP

Fiscal Spending: High Debt Stock, Expansionary Fiscal Policy, BOJ reducing bond purchases.

1. 3trn supplementary budget for energy/living cost subsidiary. PM said they won’t issue more bonds, since they will use higher tax, non-tax revenue, underspending to offset. Market was worrying about higher bond issuance, and 10y JGB yield was pushed to 2.8% (highest level since 1996)
2. MOF FY2026 JGB issuance plan focus on cut super-long supply. FY2026 (4/1/2026-3/31/2027) is set at 180.7 trillion yen (a decrease of 8.9 trillion yen compared to FY2025 supplementary budget). Issuance of super-long-term bonds (40-, 30-, and 20-year bonds) will be reduced by 100 billion yen per month, while issuance of medium-to-long-term bonds (2-, 5-, and 10-year bonds) will be maintained at the scale of FY2025 supplementary budget.
3. BOJ: Due to bond market volatility goes up, BoJ is considering stop taper in FY2027. Under current QT plan, BOJ will reduce 200bn monthly JGB purchase every quarter. However, 10y JGB yield is approaching 3%, make market even more focus on if BoJ will slow QT.
[https://www.mof.go.jp/english/policy/jgbs/publication/newsletter/](https://www.mof.go.jp/english/policy/jgbs/publication/newsletter/)

Bond Issuance by MOF and BOJ operation

1. BOJ: 1) outright JGB purchases (rinban operations) 2) fixed rate purchases 3) securities lending facility.
   1. Rinban: Outright JGB purchases, with no conditions stating that it will resell the bonds after a set period. BOJ involved in competitive auctions. **Unlike UST, BOJ accept bids starting with the highest yield bid, followed by the second highest and so on**. Schedule: BOJ announces the amounts and schedule for its outright purchases in the next quarter at quarter end. Outcome: 1) bid-to-cover ratio 2) the tail (the spread between the pro-rata yield spread and the average successful spread)
   2. Fixed rate purchase operations: it positioned this tool for achieving YCC. Now quit alr.
   3. Securities Lending Facility: JGB with repurchase agreements and involves it temporarily supplying specific issues to stabilize the market where it foresees a potential decline in liquidity. Use: 1) when it is requested to implement an offer by one or more counterparties per issue, or 2) following natural disasters or large-scale system outages. Mechanism: Selling yields, from lowest to higher. Institutions have option to reduce repurchases also.
2. MOF JGB issuance: coupons, inflation-indexed bonds (JGBi), T-bills
   1. JGBs with coupons: MOF issues 2yr, 5yr, 10yr, 20yr, and 30yr JGBs monthly and 40yr JGBs once every two months. End of year MOF will disclose frequency and amounts for next year.
      1. As a rule, overseas investors cannot participate directly in JGB auctions. MOF schedule 2-, 5-,10-, 20-, 30- auction as conventional format, 40- and JGBi with Dutch format.
      2. When issuing new JGBs, MOF sets the nominal coupon for each issue at close to the expected market yield.
      3. Auction result: (1) bid-to-cover ratio, (2) the tail (spread between average successful yield and pro-rata yield), and (3) the lowest accepted price relative to the consensus. A fat tail is usually viewed as indicating weak demand given that JGB auction bids are accepted from the highest price downward.
      4. Liquidity enhancement auctions: These involve additional issuance of existing JGB issues where there is either a structural lack of liquidity or a temporary increase in demand results in a lack of liquidity, to facilitate trading and redress market distortions. MOF's liquidity enhancement auctions are split into three maturity ranges: 1-5, 5-15.5, and 15.5-39 years. Issuance per auction is around ¥500bn. Auctions are held monthly for the 5-15.5 year category and once every two months for other maturities.
   2. 10yr JGBi auctions: As of April 2023, it plans to issue JGBi four times a year (in February, May, August, and November), with a value of ¥250bn per issue.
      1. The principal amount for typical fixed-coupon JGBs remains constant from issuance to redemption, and the same coupon rate applies to all interest payments. In contrast, JGBis' principal amount changes in line with inflation. This means that when inflation results in an increase in the inflation-adjusted principal, interest payments also rise.
      2. JGBi principal guarantee: The key hallmark of JGBi is the principal guarantee; if the indexation coefficient (which we discuss below) falls below 1, the principal amount is redeemed at face value
      3. Calculating inflation-adjusted principal: The inflation-adjusted principal changes daily and is calculated by applying the day's indexation coefficient to the bond's face value. The coefficient on a given date is calculated by dividing the reference index on that day by the index as of the 10th day of the issue month.
      4. MOF buybacks: As of April 2023, MOF is buying back around ¥20bn in JGBi per month to maintain tight supply-demand conditions. Combined with the BOJ’s ¥60bn in monthly purchases, the two therefore absorb ¥240bn of the ¥250bn in quarterly JGBi supply
   3. T-bills: Financing bills (FB) that finance the national treasury on a short-term basis or cover temporary fund shortages in a special account, and treasury bills (TB) that finance fiscal expenditures.
      1. T-bill auctions are conducted via the above conventional (price-competitive) method.
      2. T-bill maturities: T-bills are issued with 3/6/12-month maturities; 3-month T-bills are usually issued weekly, resulting in higher issuance than other maturities (Exhibit 6, Exhibit 7). Also, as MOF explicitly states in its JGB issuance plans, it flexibly adjusts the maturity, frequency, and amount of T-bill issuance to respond to market conditions and investment requirements
      3. High overseas ownership of T-bills: According to the BOJ's quarterly Flow of Funds data, overseas investors owned around 67% of T-bills as of end-2022. They held just 6% of JGBs at the same point, underscoring the extent of their T-bill market presence. We would note that heightened USD demand allows overseas investors to receive both the US-Japan interest rate spread and a premium when they lend USD to Japanese deposit-taking corporations to raise JPY, enabling them to diversify their investments even if T-bill yields are negative.
![image10.png](<G10 Rates_media/image10.png>)

![image11.png](<G10 Rates_media/image11.png>)

TONA: Tokyo overnight average rate, very similar to SOFR, but TONA is unsecured overnight call rate, while SOFR is secured repo rate.

Repo market: Japan ASW is different from RoW, is Bond – Swap

1. Package = Buy JGB + pay fixed JPY swap + fund JGB in repo; Carry = JGB yield – JPY swap rate + TONA – Repo. Fair ASW = Repo – TONA.
   1. Buy JGB + pay fixed = bet on JP ASW lower/more negative
   2. Short JGB + rec fixed = bet on JP ASW goes higher/less negative
2. Japan ASW drivers
![image12.png](<G10 Rates_media/image12.png>)

Policy Rate: Uncollateralized Overnight Call Rate:

1. Floating Rate: TONA vs TIBOR
   1. TONA: Uncollateralized Overnight Call Rate / Tokyo Overnight Average Rate: TONA.
   2. Yen TIBOR: Japan LIBOR-type benchmark: 1 month、3 month、6 month、12 month. Contains banking credit, term liquidity, and funding premium.
   3. TORF: Term RFR. Released by quick benchmarks. TORF was forward-looking term rate, like term SOFR and SOFR.

![image13.png](<G10 Rates_media/image13.png>)


<div style="page-break-after: always;"></div>


# AU

Fiscal Spending: Deficit not extreme

1. For ACGB market, supply scale is also important. 2026-27 Budget shows that underlying cash deficit is 1% of GDP, gross debt is expected rise from 982bn to 1.05trn, takes 34% of GDP.
2. AOFM weekly transaction: nominal Treasury Bond; Treasury Notes; Indexed Bonds. Treasury Notes is like Bills; Indexed Bonds is inflation bond. Scale normally smaller.
[https://www.aofm.gov.au/program/issuance-program](https://www.aofm.gov.au/program/issuance-program)

[https://www.aofm.gov.au/program/forthcoming-transactions](https://www.aofm.gov.au/program/forthcoming-transactions)

Australia Money market and front-end rates

1. RBA:
   1. Mandate of RBA: (i) the stability of the currency of Australia; (ii) the maintenance of full employment in Australia; and (iii) the economic prosperity and welfare of the people of Australia. Since the early 1990s, the RBA and Australia’s Treasury have also agreed an inflation target of 2-3%.
   2. RBA restricts its routine operations to the very front end of the money market (overnight, interbank loans, short-dated secured financing)
   3. RBA pay ESA accounts ES rate every day, which is set at 10bps below the cash target rate, considered as the lower bound of RBA’s policy-rate corridor. Ceiling of the policy corridor is the overnight standing facility repo rate, which is 25bps above the cash rate target.
![image14.png](<G10 Rates_media/image14.png>)

   4. The most widely recognized of the RBA’s policy rates is the target cash rate, RBA influences the cash rate through its open market operations, which supply or drain ESA balances and therefore determine the supply/demand of cash in the overnight, interbank market.
   5. The RBA uses repo operations to implement monetary policy by managing the amount of liquidity in the banking system, mainly through Exchange Settlement Account balances. When the banking system needs cash, the RBA can provide funds through reverse repo, lending cash against eligible collateral and increasing ESA balances. This helps ease funding pressure and keeps the overnight cash rate close to the RBA’s cash rate target. When there is excess liquidity, the RBA can drain ESA balances through repo-style operations, reducing cash in the system and supporting the cash rate. In this way, repo operations allow the RBA to control short-term money market conditions and transmit its policy stance to broader interest rates.
   6. Balance Sheet Policy: BPP; YCC, TFF.
      1. TFF offered three years of secured financing to commercial banks at 0.1%, it is a term repo.
      2. AOFM drains ESA balances by increasing their funding program. In practical terms, the AOFM will ordinarily pre-fund large maturities so there is unlikely to be a large change in ESA balances on the day of a maturity but a by allowing bonds to mature without reinvestment, the RBA increases the AOFM’s funding task and in so doing reduces the overall size of ESA balances.
      3. Future of the balance-sheet policy: An increase in the price of new OMO repos to 10bps (from 5bps) over the cash rate target, The introduction of a 7-day term, in addition to the existing 28-day term. These changes mean the RBA would not be required to hold a sizeable buffer of reserves over underlying demand. The transition from an ‘excess reserves’ to an ‘ample reserves’ regime is designed to reduce risk to the RBA (primarily, interest-rate risk) by reducing the size of the RBA’s balance sheet and trim the size of the RBA’s footprint in private markets. In so doing, the RBA intends to transition from a de facto floor system to a corridor system – the trade-off is that there will likely be more cash-rate volatility in an ‘ample reserves’ vs ‘excess reserves’ regime. RBA is expected to change interest rate corridor to be a symmetric one.
2. Products: signal-currency basis, cross-currency basis and repo
   1. BOB (Bank Bills-OIS basis): The spread between bank bills and overnight indexed swaps (OIS), measured in basis points, is **an important measure of tightness because it measures the unsecured credit risk** of Australia’s major banks. (ANZ, Westpac, NAB, CBA)
      1. Bank bills and BBSW benchmark rates: widely used reference rate in the swap market.

![image15.png](<G10 Rates_media/image15.png>)

      2. BOB: By measuring the spread to OIS, we strip out the effect of future cash-rate expectations on market prices, and we are left with a residual credit risk component: wider bob spread indicates tighter funding markets because the expected premium over cash rates for prime banks to issue is higher. Calculation: OIS reference the interbank cash rate, compounded daily until expiry and paid 2 business days after the expiry date of the swap. AONIA rate is an alternative benchmark, equivalent to OIS. The ASX offers 90-day bank bill futures contracts. Contracts start on the second Thursday of March, June, September, and December each year. Each of these months is signified by a letter: H (March), M (June), U (September) and Z (December). ASX bank bill futures contracts are generally categorized into ‘packs’ based on their proximity to the spot contract.
   2. 6s3s - In Australia, we use the term ‘6s3s’ to describe the spread between 6- month and 3-month bank bills. In some other G10 markets, a similar spread between 3 and 6-month interest-rate products is referred to as ‘3s6s’.
      1. Flow: since long-dated swaps reference 6-month, cross-currency basis swaps reference 3-month. For example, A kangaroo bond issuer doesn’t want AUD floating exposure, it wants USD dominated funding. So they need: 1. Rec AUD IRS, pay AUD 6m BBSW; 2. Pay 6s3s, adjust 6m BBSW exposure to 3m. 3. Rec AUD 3m BBSW, pay USD SOFR + basis.
      2. To calculate 6s3s, we cannot use 6-month bank bills minus 3-month directly, we need 3m3m BBSW from forward curve. 6m 6s3s = 6m BBSW - synthetic 6m rate from two 3m BBSW periods, means 6-month funding vs 3-month funding twice funding premium.
      3. Front-end drivers: spot spread, long-dated more driven by issuance-related flows.
![image16.png](<G10 Rates_media/image16.png>)

In year, RBA did a 3 consecutive times rate hike, each time 25bps, Since Jan, long AUD exposure is extremely crowded, due to 1. Commodities 2. Hike expectation from high inflation. So, in Feb, RBA did a 25-bps hike, rising interest rate from 3.6% to 3.85%.

In Mar, RBA did another hike, due to Iran conflict and high oil price. Market was priced in before the meeting starts, although the 5:4 vote leads AUDUSD down 30 pips, the hawkish tone by Bullock supports AUD. Rationale for rate hike: high inflation not only from energy, but also from AU services inflation and wage inflation. The dissent was mostly from timing; all members agree high inflation. For employment, Bullock thinks 4.1% UE still need be cooler. Forward guidance is hawkish, expressing the hiking cycle may continue.

End of Mar, AUD drop from 0.72 to 0.68, 1. Risk off sentiment with escalated Iran conflict. 2. Fundamental relative advantage was declining. The reason why AUD be strong is due to high inflation and hawkish RBA. 3. Global CB all being hawkish 4. Commodity Price

Understanding of RBA monetary policy: demand-driven inflation (domestic local demand and strict labor market), RBA thinks is stickier than imported inflation.

Long-end: about 5%, correlated with oil price. However, considering AU is LNG exporter, the energy production made AU less affected by Iran. AU pension fund buys AUD, the strong AUD offset inflation premium.

Market was doing curve flattener trade, betting when Iran issue settled, the term premium would decrease; RBA hawkish support front-end.

5 May, RBA hike again, 8:1. 25bps to 4.35%, keep supporting AUD.

With the global interest rate logic switching to higher for longer, AUD rates may steepener again. H2 with tax cut and fiscal budget, core inflation and long term premium may be pushed higher. While for front-end AOFM supply decrease and hike expectation relatively priced in.

RBA mandate: price stability and full employment. The inflation target is CPI 2%-3%. RBA especially look trimmed mean CPI.

Repo market:

1. Australian UST: ACGB: Australian Commonwealth Government Bond. ACGB ASW = AUD Swap Rate – ACGB Yield.
   1. ASW Package: Buy ACGB, pay fixed AUD swap, fund ACGB in repo. So Carry = ACGB yield – AUD swap rate + floating index – repo
   2. Carry = Floating index – repo – ASW. Fair ASW = Floating Index – Repo
   3. While US use OIS ASW, AU would like to use OIS/IRS. If use AONIA OIS swap, then floating index would be AONIA/RBA cash-rate related overnight rate. If use IRS ASW, the floating leg would be BBSW. Since BBSW was not really risk-free overnight rate, while it includes funding/credit/liquidity.
2. Trade ASW tighter: Short ACGB, rec fixed AUD Swap; Trade ASW widener: Buy ACGB, pay fixed AUD swap.
3. ACGB ASW Drivers:
![image17.png](<G10 Rates_media/image17.png>)


Policy Rate: Cash Rate Target: Unsecured overnight loans, is AUD’s near-risk-free benchmark rate, called AONIA.

Floating Rate: AONIA/Cash Rate: overnight RFR, used for AUD OIS, RBA meeting pricing, cash rate futures and discounting

BBSW: Bank Bill Swap Rate: Important Bank Credit Benchmark.

![image18.png](<G10 Rates_media/image18.png>)


<div style="page-break-after: always;"></div>


# Rates Basics

USD rates curve construction

Bootstrapping

*Risk calculation method*

*Different instruments used in IR market*

Curve strategies

Economy movers

*Carry/Roll*

<div style="page-break-after: always;"></div>


# Terms

cheap = price cheap = yield higher

rich = price expensive = yield lower

bear steepen: yield go higher; bull steepen: yield go lower

butterfly belly richens: belly yield will relatively decrease

butterfly belly cheapens: belly yield will relatively increase
