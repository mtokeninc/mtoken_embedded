# MToken Embedded System

## Introduction

MToken is an open framework for ultra low latency data, model processing and management that demands speed and capacity.  


## Subsystem

### Financial Application in a FPGA
- Market Data Feed
- Pre-Trade/Post-Trade Analytics 
- Order Routing and Execution
- Order Matching and Venue Connectivity API 
- OTC Flow Message Management
- Trading Risk Control (Limit, Circuit Breaks...)
- STP/Trade Capture
- Position, P&L, Book Management
- Risk Management (VaR)
- Clearing and Settlement
- Stress/Scenarios Testing
- Regulatory Reportings 


### Data Prcocessing in a FPGA
- Data Warehousing, Data Mining
- ETL
- Data Aggregation
- Data Routing
- Inference with Model Engine


### Media Content Processing in a FPGA
- Image
- Audio
- Video


## Architecture

### Data Prcocessing

```
┌─────────────────────────────────────────────────────────────┐
│                           MToken                            │
│                   FPGA Data Platform Pipieline              │
└─────────────────────────────────────────────────────────────┘


┌──────────────---┐      ┌────────────---─┐     
│   Data Packet   |      |  Data Packet   |
|    Ingestion    │───-─▶│    Filter      | 
│      FPGA 1     |      │     FPGA 2     |
└──────────────---┘      └──────────────--┘
                                │
         ┌─--------───────────------─--------------------┐              
         |                      |                        |
┌────────▼─────---┐     ┌───────▼─--─────-┐     ┌────────▼────---┐
│   Data Field 1  |     |   Data Field 2  |     |   Data Field n |
|    Extraction   │     │    Extraction   |     │    Extraction  | 
│      FPGA 3     |     │     FPGA 4      |     │     FPGA 2+n   |
└──────────────---┘     └──────────────---┘     └──────────────--┘
                                │
         ┌─--------───────────------─--------------------┐              
         |                      |                        |
┌────────▼─────---┐     ┌───────▼─--─────-┐     ┌────────▼────---┐
│   Data Field 1  |     |   Data Field 2  |     |   Data Field n |
|    Transform    │     │    Transform    |     │    Transform   | 
│    FPGA 3+n     |     │     FPGA 4+n    |     │   FPGA 2+2*n   |
└──────────────---┘     └──────────────---┘     └──────────────--┘ 
                                 |    
                        ┌───────-▼────────┐
                        │   Data Fields   │ 
                        │   Aggregation   │
                        │   FPGA 3+2*n    │
                        └─────────────────┘
                                 |    
                        ┌────────▼────────┐
                        │      Data       |
                        |     Router      │ 
                        │   FPGA 4+2*n    |
                        └─────────────────┘
                                 |
                                 |
                                 |
         ┌─--------───────────------─--------------------┐              
         |                       |                       |
┌────────▼─────---┐     ┌───────-▼─-─────-┐     ┌────────▼────---┐
│     Model 1     |     |     Model 2     |     |    Model m     |
|                 |     │                 |     │                | 
│    FPGA 5+2*n   |     │     FPGA 6+2*n  |     │   FPGA 4+2*n+m |
└──────────────---┘     └──────────────---┘     └──────────────--┘ 

```


## Technologies


