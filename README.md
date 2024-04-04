# DAX Measure code uding INTERSECT
SUMX(
    ADDCOLUMNS(
    SUMMARIZE(Data,
    'Date'[Date (bins)],
    Data[Product],
    Data[UserID]),
    "Service upgraded",
        VAR ItsBaseTablePM=
            CALCULATETABLE(
                SUMMARIZE(Data,
                    Data[Product],
                    Data[UserID]
        ),
        Data[Version]="Base Version",
        PREVIOUSMONTH('Date'[Date])
)
VAR PrfVersionTable=
    CALCULATETABLE(
        SUMMARIZE(Data,
            Data[Product],
            Data[UserID]
        ),
        Data[Version]="Professional Version")
RETURN
   COUNTROWS(INTERSECT(ItsBaseTablePM,PrfVersionTable))),[Service upgraded])
