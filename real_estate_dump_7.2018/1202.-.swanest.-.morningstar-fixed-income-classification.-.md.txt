Morningstar Fixed Income Classification System Map (MFICS)
==========================================================

This library just aims to enable lookups in the reference table of Morningstar as published on their [website](http://corporate.morningstar.com/us/documents/MethodologyDocuments/MethodologyPapers/MorningstarGlobalFixedIncomeClass.pdf) in an easy way by building a Node module containing a JSON map and some methods to explore it.

## Installation

```shell
npm install morningstar-fixed-income-classification
```

## Usage

```javascript
var MFICS = require('morningstar-fixed-income-classification');

MFICS.all()
/*=> [ { name: 'Government',
         code: 10,
         type: 'Super Sector',
         description: 'This Super Sector includes all conventional debt issued by governments, bonds issued by a Central Bank or Treasury, and bonds issued by local governments, cantons, regions and provinces.' }, ...]
*/

MFICS.search('finance');
/*=> [ { name: 'Transportation',
         code: 2020100,
         type: 'Secondary Sector',
         primarySector: 2020,
         superSector: 20,
         description: 'Transportation-related municipal bonds finance all sorts of projects, including non-toll and toll-backed road, bridge, and tunnel construction. They may also finance airport and seaport construction, recurring maintenance of intra-county and city public transportation systems, and more. They may be backed by taxes, tolls, ridership fees, and more.',
         score: 1 },
       { name: 'Utilities',
         code: 2020300,
         type: 'Secondary Sector',
         primarySector: 2020,
         superSector: 20,
         description: 'Utility-related municipal bonds finance construction and maintenance of power plants, electrical grids, telephone grids, and more. Their source of backing varies but may include property taxes, usage fees, and more.',
         score: 1 },
       { name: 'Miscellaneous Revenue',
         code: 2020400,
         type: 'Secondary Sector',
         primarySector: 2020,
         superSector: 20,
         description: 'This category describes harder-to-categorize municipal bonds that may finance a wide variety of projects.',
         score: 1 } ]
*/

MFICS.find('2020100');
/*=> { name: 'Water & Sewer',
       code: 2020100,
       type: 'Secondary Sector',
       superSector: 20,
       primarySector: 2020,
       description: 'These municipal bonds are similar to utility-related issues. They provide initial financing for construction of water and sewer systems that property taxes or other income will eventually repay.' }
*/

MFICS.above('2020100');
/*=> [ { name: 'Transportation',
         code: 2020100,
         type: 'Secondary Sector',
         primarySector: 2020,
         superSector: 20,
         description: 'Transportation-related municipal bonds finance all sorts of projects, including non-toll and toll-backed road, bridge, and tunnel construction. They may also finance airport and seaport construction, recurring maintenance of intra-county and city public transportation systems, and more. They may be backed by taxes, tolls, ridership fees, and more.' },
       { name: 'Municipal Tax-Exempt',
         code: 2020,
         type: 'Primary Sector',
         superSector: 20,
         description: 'Local governments, state governments, provinces, and regional authorities are often referred to more generally as "municipalities" and typically issue bonds in order to raise money for operations and development. This financing is sometimes used to build or upgrade hospitals, sewer systems, schools, housing, stadiums, or industrial complexes. Some municipal bonds are backed by the issuing entity, while others are linked to a revenue stream, such as from a toll way or a utility. Municipal bonds in the United States are typically exempt from federal taxes and often the taxes of the states in which they are issued. Those taxation advantages may allow municipal governments to sell bonds at lower interest rates than those offered by comparable taxable bonds. This Primary Sector includes issues that are subject to the Alternative Minimum Tax but not other federal taxes. Corporate' },
       { name: 'Municipal',
         code: 20,
         type: 'Super Sector',
         description: 'The Municipal Super Sector includes taxable and tax-exempt debt obligations issued under the auspices of states, cities, counties, provinces, and other non-federal government entities.' } ]
*/

MFICS.below('9261');
/*=> [ { name: 'Preferred Stock',
          code: 3040,
          type: 'Primary Sector',
          superSector: 30,
          description: 'Preferred stock is legally structured as equity, above common equity in a company\'s capital structure, but does not offer voting rights. Preferred stock often pays a fixed dividend and has priority over common equity when an issuing company elects to pay dividends. Although preferred stocks are not debt instruments, investors often treat them as such because of their income payouts and higher capital-structure placement. Securitized' },
        { name: 'Health-Care',
          code: 3040100,
          type: 'Secondary Sector',
          primarySector: 3040,
          superSector: 30,
          description: 'This Secondary Sector includes biotechnology, pharmaceuticals, research services, home health-care, hospitals, long-term-care facilities, and medical equipment and supplies.' },
        { name: 'Industrials',
          code: 3040200,
          type: 'Secondary Sector',
          primarySector: 3040,
          superSector: 30,
          description: 'Companies that manufacture machinery, hand-held tools, and industrial products. This Secondary Sector also includes aerospace and defense firms as well as companies engaged in transportations and logistic services.' },
        { name: 'Real Estate',
          code: 3040300,
          type: 'Secondary Sector',
          primarySector: 3040,
          superSector: 30,
          description: 'This sector includes mortgage companies, property management companies, and REITs.' },
        { name: 'Utilities',
          code: 3040400,
          type: 'Secondary Sector',
          primarySector: 3040,
          superSector: 30,
          description: 'Electric, gas, and water utilities. Companies in this Secondary Sector include Electricité de France, Exelon Corporation, and PG&E Corporation.' },
        { name: 'Unspecified',
          code: 3040500,
          type: 'Secondary Sector',
          primarySector: 3040,
          superSector: 30,
          description: 'Corporate sector designation could not be determined.' },
        { name: 'Agency Pass-Through',
          code: 3040600,
          type: 'Secondary Sector',
          primarySector: 3040,
          superSector: 30,
          description: 'These are securities that represent a claim on the cash flows associated with a pool of mortgages. Pass-through bondholders are entitled to a pro-rata share of the principal and interest payments paid by the homeowners. The timely payment of principal and interest for agency pass-through securities is guaranteed by government agencies. The underlying collateral of bonds in this Secondary Sector are fixed-rate mortgages; bonds backed by adjustable-rate mortgages are included in the Agency ARM Secondary Sector.' } ]
*/
```

## Dataset Indexing

In order to enable keyword-based searches on the MFICS dataset, we use a reverse index stored in ``/data/data-index.json``. The index is generated by tokenizing relevant properties on MFICS classifications and storing them in an index object keyed by the tokenized text. The index relates keywords to scores that represent the likelihood that a specific keyword is related to a MFICS classification.

In order to rebuild the index run the following command from the project directory:

```shell
$ ./bin/build-index.js
```

Most of the work comes from [@lovehandle/naics-2012](https://github.com/lovehandle/naics-2012)