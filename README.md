# peerfinder

[![Build Status](https://travis-ci.org/rucarrol/PeerFinder.png)](https://travis-ci.org/rucarrol/PeerFinder)

## Installation

peerfinder can be installed via PIP:

```
$ pip3 search peerfinder
peerfinder (2020.7.25)  - A tool to find common IX points as per PeeringDB
```
Failing that, you an build from source and install locally:
```
git clone https://github.com/rucarrol/PeerFinder.git
cd PeerFinder
python3 setup.py sdist bdist_wheel
pip install ./dist/peerfinder*.whl
```


## Usage

PeerFinder is a python3.7 and beyond script which finds common points of presence between ASNs as reported by [PeeringDB](peeringdb.com). 

The tool takes a mandatory arguments: `--asn`. There are three arguments to control output: `--ix`,  `--private` and `--missing`.

```
$ peerfinder --asn 2603 13414 --ix --private
Fetching PeeringDB info for 2603
Fetching PeeringDB info for 13414
+-----------------------------------------------------+-----------------------------+-----------------------------+
|                          IX                         |           NORDUnet          |        Twitter, Inc.        |
+-----------------------------------------------------+-----------------------------+-----------------------------+
|                        AMS-IX                       |      v4: 80.249.209.203     |      v4: 80.249.208.130     |
|                                                     | v6: 2001:7f8:1::a500:2603:1 |        80.249.210.46        |
|                                                     |                             | v6: 2001:7f8:1::a501:3414:1 |
|                                                     |                             |   2001:7f8:1::a501:3414:2   |
+-----------------------------------------------------+-----------------------------+-----------------------------+
|    DE-CIX Frankfurt: DE-CIX Frankfurt Peering LAN   |      v4: 80.81.192.241      |       v4: 80.81.192.10      |
|                                                     |    v6: 2001:7f8::a2b:0:1    |         80.81.194.21        |
|                                                     |                             |    v6: 2001:7f8::3466:0:1   |
|                                                     |                             |      2001:7f8::3466:0:2     |
+-----------------------------------------------------+-----------------------------+-----------------------------+
|                   Equinix Ashburn                   |     v4: 206.126.236.230     |      v4: 206.126.236.97     |
|                                                     |   v6: 2001:504:0:2::2603:1  | v6: 2001:504:0:2:0:1:3414:2 |
+-----------------------------------------------------+-----------------------------+-----------------------------+
|                   Equinix Chicago                   |     v4: 208.115.136.151     |     v4: 208.115.136.171     |
|                                                     |   v6: 2001:504:0:4::2603:1  | v6: 2001:504:0:4:0:1:3414:1 |
+-----------------------------------------------------+-----------------------------+-----------------------------+
|                HKIX: HKIX Peering LAN               |      v4: 123.255.91.213     |      v4: 123.255.90.149     |
|                                                     |                             | v6: 2001:7fa:0:1::ca28:a095 |
+-----------------------------------------------------+-----------------------------+-----------------------------+
|                   LINX LON1: Main                   |      v4: 195.66.225.24      |      v4: 195.66.225.142     |
|                                                     |    v6: 2001:7f8:4::a2b:1    |        195.66.226.61        |
|                                                     |                             |    v6: 2001:7f8:4::3466:1   |
|                                                     |                             |      2001:7f8:4::3466:2     |
+-----------------------------------------------------+-----------------------------+-----------------------------+
|                     LONAP: LON0                     |       v4: 5.57.80.168       |        v4: 5.57.81.31       |
|                                                     |    v6: 2001:7f8:17::a2b:1   |          5.57.81.32         |
|                                                     |                             |   v6: 2001:7f8:17::3466:1   |
|                                                     |                             |     2001:7f8:17::3466:2     |
+-----------------------------------------------------+-----------------------------+-----------------------------+
|  Netnod Stockholm BLUE -- MTU1500: STH-B -- MTU1500 |      v4: 194.68.128.24      |      v4: 194.68.128.229     |
|                                                     |    v6: 2001:7f8:d:fe::24    |    v6: 2001:7f8:d:fe::229   |
+-----------------------------------------------------+-----------------------------+-----------------------------+
|  Netnod Stockholm BLUE -- MTU4470: STH-B -- MTU4470 |      v4: 195.69.119.24      |      v4: 195.69.119.229     |
|                                                     |    v6: 2001:7f8:d:fb::24    |    v6: 2001:7f8:d:fb::229   |
+-----------------------------------------------------+-----------------------------+-----------------------------+
| Netnod Stockholm GREEN -- MTU1500: STH-A -- MTU1500 |      v4: 194.68.123.24      |      v4: 194.68.123.229     |
|                                                     |    v6: 2001:7f8:d:ff::24    |    v6: 2001:7f8:d:ff::229   |
+-----------------------------------------------------+-----------------------------+-----------------------------+
| Netnod Stockholm GREEN -- MTU4470: STH-A -- MTU4470 |      v4: 195.245.240.24     |     v4: 195.245.240.229     |
|                                                     |    v6: 2001:7f8:d:fc::24    |    v6: 2001:7f8:d:fc::229   |
+-----------------------------------------------------+-----------------------------+-----------------------------+
+----------------------------------------------------+-----------+---------------+
|                      Facility                      |  NORDUnet | Twitter, Inc. |
+----------------------------------------------------+-----------+---------------+
|           Equinix CH1/CH2/CH4 - Chicago            | ASN: 2603 |   ASN: 13414  |
+----------------------------------------------------+-----------+---------------+
|             Equinix DC1-DC15 - Ashburn             | ASN: 2603 |   ASN: 13414  |
+----------------------------------------------------+-----------+---------------+
|          Equinix LD8 - London, Docklands           | ASN: 2603 |   ASN: 13414  |
+----------------------------------------------------+-----------+---------------+
| Interxion Stockholm (STO1, STO2, STO3, STO4, STO5) | ASN: 2603 |   ASN: 13414  |
+----------------------------------------------------+-----------+---------------+

```

## --missing

The cli switch to print the IXPs in which the given list of ASNs are not present in, and report the port speed if the present peer.

eg:
```peerfinder --asn 2603 13414 --missing
Fetching PeeringDB info for 2603
Fetching PeeringDB info for 13414
+----------------------------------------------------+----------------+---------------------+
|                         IX                         | NORDUnet speed | Twitter, Inc. speed |
+----------------------------------------------------+----------------+---------------------+
|                   Equinix Dallas                   |                |      40000Mbit      |
+----------------------------------------------------+----------------+---------------------+
|                     BBIX Tokyo                     |                |      400000Mbit     |
+----------------------------------------------------+----------------+---------------------+
|                Equinix Los Angeles                 |                |      30000Mbit      |
+----------------------------------------------------+----------------+---------------------+
|                   Equinix  Miami                   |                |      30000Mbit      |
+----------------------------------------------------+----------------+---------------------+
|               SIX Seattle: MTU 1500                |                |      20000Mbit      |
+----------------------------------------------------+----------------+---------------------+
|           SIX Seattle (Jumbo): MTU 9000            |                |      20000Mbit      |
+----------------------------------------------------+----------------+---------------------+
|               MegaIX Sydney: MegaIX                |                |      20000Mbit      |
+----------------------------------------------------+----------------+---------------------+
|         IX.br (PTT.br) São Paulo: ATM/MPLA         |                |      20000Mbit      |
+----------------------------------------------------+----------------+---------------------+
|         IX Australia (Sydney NSW): NSW-IX          |                |      20000Mbit      |
+----------------------------------------------------+----------------+---------------------+
|                  France-IX Paris                   |                |      20000Mbit      |
+----------------------------------------------------+----------------+---------------------+
|      Equinix São Paulo: Equinix IX - SP Metro      |                |      20000Mbit      |
+----------------------------------------------------+----------------+---------------------+
|                   Equinix Sydney                   |                |      20000Mbit      |
+----------------------------------------------------+----------------+---------------------+
|       Equinix London: Equinix IX - LD Metro        |                |      20000Mbit      |
+----------------------------------------------------+----------------+---------------------+
|      Equinix Frankfurt: Equinix IX - FR Metro      |                |      20000Mbit      |
+----------------------------------------------------+----------------+---------------------+
|      Equinix Amsterdam: Equinix IX - AM Metro      |                |      20000Mbit      |
+----------------------------------------------------+----------------+---------------------+
|      DE-CIX Madrid: DE-CIX Madrid Peering LAN      |                |      20000Mbit      |
+----------------------------------------------------+----------------+---------------------+
|                JPNAP Tokyo: Peering                |                |      200000Mbit     |
+----------------------------------------------------+----------------+---------------------+
|                   Equinix Tokyo                    |                |      200000Mbit     |
+----------------------------------------------------+----------------+---------------------+
|                 Equinix Singapore                  |                |      200000Mbit     |
+----------------------------------------------------+----------------+---------------------+
|                  Equinix San Jose                  |                |      200000Mbit     |
+----------------------------------------------------+----------------+---------------------+
|                 Equinix Palo Alto                  |                |      200000Mbit     |
+----------------------------------------------------+----------------+---------------------+
|                  Equinix New York                  |                |      200000Mbit     |
+----------------------------------------------------+----------------+---------------------+
|               Digital Realty Atlanta               |                |      200000Mbit     |
+----------------------------------------------------+----------------+---------------------+
|             CoreSite - Any2 California             |                |      200000Mbit     |
+----------------------------------------------------+----------------+---------------------+
|              DE-CIX Johor Bahru: JBIX              |                |        10Mbit       |
+----------------------------------------------------+----------------+---------------------+
|                        MyIX                        |                |       1000Mbit      |
+----------------------------------------------------+----------------+---------------------+
|                 Equinix Hong Kong                  |                |      10000Mbit      |
+----------------------------------------------------+----------------+---------------------+
|              ESPANIX Madrid Upper LAN              |                |      10000Mbit      |
+----------------------------------------------------+----------------+---------------------+
|              ESPANIX Madrid Lower LAN              |                |      10000Mbit      |
+----------------------------------------------------+----------------+---------------------+
|                  AMS-IX Hong Kong                  |                |      10000Mbit      |
+----------------------------------------------------+----------------+---------------------+
|           STHIX - Stockholm: STH Peering           |   20000Mbit    |                     |
+----------------------------------------------------+----------------+---------------------+
|          STHIX - Copenhagen: CPH Peering           |   10000Mbit    |                     |
+----------------------------------------------------+----------------+---------------------+
|                 SGIX: Peering LAN                  |   10000Mbit    |                     |
+----------------------------------------------------+----------------+---------------------+
|                        RIX                         |   10000Mbit    |                     |
+----------------------------------------------------+----------------+---------------------+
|     Netnod Copenhagen GREEN -- MTU9K: 9K-GREEN     |   10000Mbit    |                     |
+----------------------------------------------------+----------------+---------------------+
|      Netnod Copenhagen BLUE -- MTU9K: 9K-BLUE      |   10000Mbit    |                     |
+----------------------------------------------------+----------------+---------------------+
|                       NYIIX                        |   10000Mbit    |                     |
+----------------------------------------------------+----------------+---------------------+
|                    NL-ix: Main                     |   10000Mbit    |                     |
+----------------------------------------------------+----------------+---------------------+
|                        NIX1                        |   10000Mbit    |                     |
+----------------------------------------------------+----------------+---------------------+
|                      ECIX-HAM                      |   10000Mbit    |                     |
+----------------------------------------------------+----------------+---------------------+
|                      ECIX-FRA                      |   10000Mbit    |                     |
+----------------------------------------------------+----------------+---------------------+
|                    DIX: DIX LAN                    |   10000Mbit    |                     |
+----------------------------------------------------+----------------+---------------------+
|                        CIXP                        |   10000Mbit    |                     |
+----------------------------------------------------+----------------+---------------------+
| Asteroid Amsterdam: Asteroid Amsterdam Peering LAN |   10000Mbit    |                     |
+----------------------------------------------------+----------------+---------------------+
```

## Bugs, Features 

Please open a PR!