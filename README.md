# Pip Value Calculator MT4 Indicator
![Pip-Value-Calculator Screen](https://forexnew.org/Download/Pip-Value-MT4-Indicator.png)
- Indicator to automate Forex pip value calculations.
- Coding for MetaTrader 4 Platform.
- See working example at [Pip Value Indicator MT4](https://forexnew.org/คลังความรู้/pip-value-การคำนวน-lot/#indicators)

## Formula
- Pip Value = (One Pip ÷ Exchange Rate) x Lot Size

## Inputs Parameter
![Pip-Value-MT4-Inputs](https://forexnew.org/Download/pip-value-mt4-input.png)
- Default Lot Size : 1.00
- Text Size : 9
- Text Color : MintCream
- Panel Color : SteelBlue
- Decimal : 2

## MQL4 Code

```
#property copyright    "ForexNew.org Opensource"
#property link         "https://forexnew.org/"
#property version      "1.10"
#property description  "Pip Value Calculator For MetaTrader 4"
#property strict
#property indicator_chart_window

// Input parameters //
extern double Lot_Size=1.00;   // Default Lot Size
extern int Text_Size=9;  // Text Size
extern int decimal=2; //Decimal
extern color Text_Color=MintCream;  // Text Color
extern color Panel_Color=SteelBlue;  // Panel Color
string Font_Setting="Arial Black";
double point;

// Check symbol digits //
int OnInit()
{
   point=Point;
   if((Digits==3) || (Digits==5))
   {
      point*=10;
   }
   return(INIT_SUCCEEDED);
}

// Calculation function, Reference: https://www.mql5.com/en/docs/event_handlers/oncalculate //
int OnCalculate(const int rates_total,
                const int prev_calculated,
                const datetime &time[],
                const double &open[],
                const double &close[],
                const double &high[],
                const double &low[],
                const long &volume[],
                const long &tick_volume[],
                const int &spread[])
  {
   string Account_Currency=AccountInfoString(ACCOUNT_CURRENCY);
   double PipValue_Total=((((MarketInfo(Symbol(),MODE_TICKVALUE)*point)/MarketInfo(Symbol(),MODE_TICKSIZE))*Lot_Size));

// Create panel and text Label on the screen //
   ObjectCreate("Main_Panel",OBJ_RECTANGLE_LABEL,0,0,0,0,0,0);
   ObjectSet("Main_Panel",OBJPROP_BGCOLOR,Panel_Color);
   ObjectSet("Main_Panel",OBJPROP_CORNER,0);
   ObjectSet("Main_Panel",OBJPROP_BACK,true);
   ObjectSet("Main_Panel",OBJPROP_XDISTANCE,10);
   ObjectSet("Main_Panel",OBJPROP_YDISTANCE,20);
   ObjectSet("Main_Panel",OBJPROP_XSIZE,240);
   ObjectSet("Main_Panel",OBJPROP_YSIZE,95);
   ObjectSet("Main_Panel", OBJPROP_SELECTABLE, false);
   ObjectSet("Main_Panel", OBJPROP_HIDDEN, true);
   
   ObjectCreate("Label_1", OBJ_LABEL, 0, 0, 0);
   ObjectSetText("Label_1","- Symbol : " + Symbol(),Text_Size,Font_Setting, Text_Color);
   ObjectSet("Label_1", OBJPROP_CORNER, 0);
   ObjectSet("Label_1", OBJPROP_XDISTANCE, 20);
   ObjectSet("Label_1", OBJPROP_YDISTANCE, 27);
   ObjectSet("Label_1", OBJPROP_SELECTABLE, false);
   ObjectSet("Label_1", OBJPROP_HIDDEN, true);
   
   ObjectCreate("Label_2", OBJ_LABEL, 0, 0, 0);
   ObjectSetText("Label_2","- Account Currency : " + Account_Currency,Text_Size,Font_Setting, Text_Color);
   ObjectSet("Label_2", OBJPROP_CORNER, 0);
   ObjectSet("Label_2", OBJPROP_XDISTANCE, 20);
   ObjectSet("Label_2", OBJPROP_YDISTANCE, 47);
   ObjectSet("Label_2", OBJPROP_SELECTABLE, false);
   ObjectSet("Label_2", OBJPROP_HIDDEN, true);
   
   ObjectCreate("Label_3", OBJ_LABEL, 0, 0, 0);
   ObjectSetText("Label_3","- Pip Value (one point) : " + DoubleToStr(PipValue_Total/10,decimal),Text_Size,Font_Setting, Text_Color);
   ObjectSet("Label_3", OBJPROP_CORNER, 0);
   ObjectSet("Label_3", OBJPROP_XDISTANCE, 20);
   ObjectSet("Label_3", OBJPROP_YDISTANCE, 67);
   ObjectSet("Label_3", OBJPROP_SELECTABLE, false);
   ObjectSet("Label_3", OBJPROP_HIDDEN, true);
   
   ObjectCreate("Label_4", OBJ_LABEL, 0, 0, 0);
   ObjectSetText("Label_4","- Pip Value (one pip) : " + DoubleToStr(PipValue_Total,decimal),Text_Size,Font_Setting, Text_Color);
   ObjectSet("Label_4", OBJPROP_CORNER, 0);
   ObjectSet("Label_4", OBJPROP_XDISTANCE, 20);
   ObjectSet("Label_4", OBJPROP_YDISTANCE, 87);
   ObjectSet("Label_4", OBJPROP_SELECTABLE, false);
   ObjectSet("Label_4", OBJPROP_HIDDEN, true);
   
   ObjectCreate("Label_5", OBJ_LABEL, 0, 0, 0);
   ObjectSetText("Label_5","Copyright: ForexNew.org - Free Opensource",9, "Arial", DeepSkyBlue);
   ObjectSet("Label_5", OBJPROP_CORNER, 2);
   ObjectSet("Label_5", OBJPROP_XDISTANCE, 10);
   ObjectSet("Label_5", OBJPROP_YDISTANCE, 10);
   ObjectSet("Label_5", OBJPROP_SELECTABLE, false);
   ObjectSet("Label_5", OBJPROP_HIDDEN, true);

   return(rates_total); 
  }
  
// Delete panel and text label when removing the indicator //
void OnDeinit(const int reason)
{
   ObjectsDeleteAll(0,"Main_Panel");
   ObjectsDeleteAll(0,"Label_1");
   ObjectsDeleteAll(0,"Label_2");
   ObjectsDeleteAll(0,"Label_3");
   ObjectsDeleteAll(0,"Label_4");
   ObjectsDeleteAll(0,"Label_5");
}
```
## Visit our website
- [ForexNew.org](https://forexnew.org/)
