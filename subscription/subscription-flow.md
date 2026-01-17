
``` mermaid
flowchart TD
    %% Node เริ่มต้น
    Start[Tenant สนใจ] --> PathDecision{เลือก Path}

    %% ทางเลือกฝั่งขวา: ซื้อเลย (เส้นยาว)
    PathDecision -- ซื้อเลย --> BuyDirect[เลือก Package + 2 เดือนฟรี]

    %% ทางเลือกฝั่งซ้าย: ทดลองก่อน
    PathDecision -- ทดลองก่อน --> Trial[Trial 1 เดือนฟรี]
    Trial --> EndTrial[หมด Trial]
    EndTrial --> SelectYearly[เลือก Package รายปี]
    
    %% จุดตัดสินใจ: การต่อรอง
    SelectYearly --> NegDecision{ต่อรอง?}
    
    %% Loop การต่อรอง
    NegDecision -- ครั้งที่ 1 --> OfferOne[+1 เดือนฟรี]
    OfferOne --> NegDecision
    
    NegDecision -- ครั้งที่ 2 --> OfferMax[+1 เดือนฟรี - MAX]
    OfferMax --> BuyPkg[ซื้อ Package]
    
    NegDecision -- ไม่ต่อรอง --> BuyPkg

    %% จุดสิ้นสุด: Active
    BuyDirect --> Active[ACTIVE Subscription]
    BuyPkg --> Active
```