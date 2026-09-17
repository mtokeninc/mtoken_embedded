# MToken Embedded System

## Introduction

MToken is an open framework for ultra low latency data, model processing and management that demands speed and capablity.  


## Subsystem

### Wall Street in a FPGA
- Market Data Feed 
- Order Routing and Execution
- Order Matching and Venue 
- OTC Flow Message Management
- Trading Risk Control (Limit, Circuit Breaks...)
- STP
- Position, P&L, Book Management
- Risk Management (VaR)
- Stress Testing
- Clearing and Settlement 


### Data Prcocessing in a FPGA
- Data Warehousing, Data Mining
- ETL
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
|    Extraction   │     │    Extraction   |     │   Aggregation  | 
│      FPGA 3     |     │     FPGA 4      |     │     FPGA 2+n   |
└──────────────---┘     └──────────────---┘     └──────────────--┘
                                │
         ┌─--------───────────------─--------------------┐              
         |                      |                        |
┌────────▼─────---┐     ┌───────▼─--─────-┐     ┌────────▼────---┐
│   Data Field 1  |     |   Data Field 2  |     |   Data Field n |
|    Transform    │     │    Transform    |     │    Transform   | 
│      FPGA 3+n   |     │     FPGA 4+n    |     │     FPGA 2+2*n |
└──────────────---┘     └──────────────---┘     └──────────────--┘ 
                                |    
                        ┌───────▼-────────┐
                        │  Data Fields    │ 
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
         |                      |                        |
┌────────▼─────---┐     ┌───────▼─--─────-┐     ┌────────▼────---┐
│     Model 1     |     |     Model 2     |     |    Model m     |
|                 |     │                 |     │                | 
│    FPGA 5+2*n   |     │     FPGA 6+2*n  |     │   FPGA 4+2*n+m |
└──────────────---┘     └──────────────---┘     └──────────────--┘ 

