# MToken Embedded System


## Introduction

MToken is an open framework for ultra low latency data, model processing and management that demands speed and capacity.  


## Subsystem

### Financial Application in a FPGA
- Venue Connectivity/API
- Real Time Market Data Feed
- Pre-Trade Analytics
- Pricing Engine
- Order Routing and Execution
- Order Matching
- OTC Flow Message Management
- Post-Trade Analytics
- Trading Risk Control (Limit, Circuit Breaks, etc)
- STP/Trade Capture
- Position, P&L, Book Management
- Risk Management (VaR)
- Clearing and Settlement
- Stress/Scenarios Testing
- Regulatory Reporting 


### Data Processing in a FPGA
- Data Mining
- ETL
- Data Aggregation
- Data Routing
- Inference with Model Engine

### Media Content Processing in a FPGA
- Image
- Audio
- Video


## Architecture

### Data Processing

```
┌─────────────────────────────────────────────────────────────┐
│                           MToken                            │
│                   FPGA Data Platform Pipeline               │
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


