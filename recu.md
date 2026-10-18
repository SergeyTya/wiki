# Структурная схема Charger to Grid преобразователя
```mermaid
flowchart TB

    %%{init: {"theme": "dark", "themeVariables": {"darkMode": true}}}%%
    %%{init: {"themeVariables": {"fontSize": "16px"}}}%%

    N1["`АКБ накопителя (предполагается то же уровень напряжения, что и у батареи EV)`"]
    N2[" DC/DC Повышает напряжение и обеспечивает гальваническую развязку. Применяется опционально. Может быть заменен на буст преобр. "] 
    N3["Накопитель энергии AFE - Коденсаторная сборка с низкоиндуктивной шиной"]
    N4["Трехфазный мостовой инвертор. Обеспечивает рекуперацию энергии в трехфазную сеть. Может быть реализован как три однофазных преобр. для работы с нейтралью"]
    N5["Обеспечивает защиту от помех"]

    N6["Применяется по требованиям ТЗ"]
    
    N1~~~N6~~~N2~~~N3~~~N4~~~N5


    ISO[" Блок конроля изоляции (Опционально)"] 
    BAT[" <b>ЭЗС</b> 🔋 <br/> АКБ 400V"] --> ISO --> LLC
      
    subgraph LLC["DC/DC — LLC-резонансный"]
        MCU_LLC["MCU LLC<br/> Контроллер"]-->HB
        direction LR
        HB["H-мост<br/> Силовая часть"] --> LR["LLC<br/>резонансный контур"]
         --> TR["HF Трансформатор"]
        TR --> RECT["Выпрямитель"]
    end
   
    LLC --> DCBUS["DC-шина 720V"] --> AFE


     
    subgraph AFE["AFE (Active Front End) "]
        %%{init: {"flowchart": {"minNodeWidth": 0, "minNodeHeight": 0}}}%%
        direction LR
        Udc(("Udc")) -->|"Напряжение <br/> DC шины"| INV
        IA --> LCL
        IB --> LCL
        IC --> LCL
        
        LCL -.->|"Напряжение <br/> фазы R"| INV
        IA -.-> |"Ток R"|INV -->|"PWM1"|IA(("Ia<br/>"))
        LCL -.->|"Напряжение <br/> фазы S"| INV
        IB -.-> |"Ток S"|INV -->|"PWM2"| IB(("Ib<br/>"))
        LCL -.->|"Напряжение <br/> фазы T"| INV
        IC -.-> |"Ток T"|INV -->|"PWM3"| IC(("Ic<br/>"))
    
    end

    subgraph INV["Активный выпрямитель"]
        direction TB
        MCU_INV["MCU AFE <br/> Контроллер"] -->
        DR["Драйвер"] -->
        BR["SiC инвертор <br/> Силовая часть"]
 
    end

    subgraph LCL["LCL-фильтр"]
        direction LR
        LF_R("LCL")~~~LF_S("LCL")~~~LF_T("LCL")
    end

   

    AFE --> EMF["EMF  <br/> Фильтр электромагнитной совместимости"]--> GRID["⚡ Сеть 3~ AC<br/>"]

    classDef note fill: #665605 ,stroke:#b7950b,stroke-dasharray: 3 3;
    class N1 note;
    class N2 note;
    class N3 note;
    class N4 note;
    class N5 note;
    class N6 note;



```
## Информационный обмен

```mermaid
flowchart TB
    MCU2["Диспетчер Сети"]
    MCU1["Контроллер <br/>  ЭЗС"]
    MCU3["Контроллер Рекуператора"]


    MCU1-->|"OCPP"|MCU2
    MCU3-->|"CAN "|MCU2
```
Информационный обмен обеспечивается через диспетчера, который определяет необходимость и обьем энергии к рекуперации. Диспетчер представляет собой SCADA систему верхнего уровня подключенной к энерго узлу.

## Пример реализации
В самом простом случае в качестве DC\DC и АFE может быть использован готовый модуль UBR100030 — 30kW Bidirectional AC/DC Power Module (https://www.uugreenpower.com/), в данном случае 4 модуля в параллель обеспечивают 120 кВт мощности. Модули управляются по CAN линии через контроллер рекуператора. 

    