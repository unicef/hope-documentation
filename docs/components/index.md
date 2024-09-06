---
title: Ecosystem
---

# Ecosystem components

HOPE is designed with a modular architecture, giving users the flexibility to customize and extend the platform according to their unique needs. It’s built to be scalable, adaptable, and interoperable, making it simple to integrate with other systems and platforms, ensuring smooth workflows and easy expansion as your needs grow.

```mermaid
    C4Context
    title Ecosystem High Level Architecture
    Enterprise_Boundary(b0, "Ecosystem") {
        Boundary(Core, "Core", "") {
            System(HOPE, "HOPE")
            SystemDb(Postgres, "Postgres")
            SystemDb(RO, "ReadOnly  ")
            Rel(HOPE, Postgres, "uses")
        }

        Boundary(Kobo, "Kobo", "") {
            SystemDb(KoboPostgres, "Postgres")
            System_Ext(Kobo, "Kobo")
        }
        Boundary(Aurora, "Aurora", "") {
            System(Aurora, "Aurora")
            SystemDb(AuroraPostgres, "Postgres")
        }
        Boundary(Services, "Services", "") {
            Boundary(DeduplicationEngine, "DeduplicationEngine", "") {
                System(DeduplicationEngine, "DeduplicationEngine")
                SystemDb(DeduplicationEnginePostgres, "Postgres")
            }
            Boundary(CountryReport, "CountryReport", "") {
                System(CountryReport, "CountryReport")
                SystemDb(CountryReportPostgres, "Postgres")
            }
            Boundary(PaymentGateway, "PaymentGateway", "") {
                System(PaymentGateway, "PaymentGateway")
                SystemDb(PGPostgres, "Postgres")
            }
        }
    }
%%      BiRel(HOPE, SystemAA, "Uses")
%%      BiRel(SystemAA, SystemE, "Uses")
%%      Rel(SystemAA, SystemC, "Sends e-mails", "SMTP")
%%      UpdateElementStyle(HOPE, $fontColor="red", $bgColor="grey", $borderColor="red")
%%      UpdateRelStyle(HOPE, SystemAA, $textColor="blue", $lineColor="blue", $offsetX="5")
%%      UpdateRelStyle(SystemAA, SystemE, $textColor="blue", $lineColor="blue", $offsetY="-10")
%%      UpdateRelStyle(SystemAA, SystemC, $textColor="blue", $lineColor="blue", $offsetY="-40", $offsetX="-50")
%%      UpdateRelStyle(SystemC, HOPE, $textColor="red", $lineColor="red", $offsetX="-50", $offsetY="20")
%%
%%      UpdateLayoutConfig($c4ShapeInRow="3", $c4BoundaryInRow="1")
```


The source code for HOPE is fully open-source and available for anyone to explore, contribute to, or customize. Our codebase is hosted on GitHub, making it easy to access, review, and collaborate on.


- [HOPE](hope/index.md)
- [Aurora](components/aurora.md)
- [Kobo](components/kobo.md)
- [Payment Gateway](pg/index.md)
- [Deduplication Engine](components/hde.md)
- [Country Report](components/reporting.md)
- [Country Workspace] _work in progress_
