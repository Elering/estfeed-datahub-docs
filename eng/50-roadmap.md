# Roadmap

## API developments

| Topic                  | Type   | Endpoint                                 | Description                                                          | Deployment |
|------------------------|--------|------------------------------------------|----------------------------------------------------------------------|------------|
| Agreement              | `POST` | /api/v1/agreement                        | Create agreement                                                     | Deployed   |
| Agreement              | `PUT`  | /api/v1/agreement                        | Update agreement                                                     | Deployed   |
| Agreement              | `POST` | /api/v1/agreement/search                 | Find agreements                                                      | Deployed   |
| Agreement              | `POST` | /api/v1/agreement/export                 | Export agreements by attributes                                      | Deployed   |
| Agreement              | `POST` | /api/v1/agreement/delete                 | Delete agreement                                                     | Deployed   |
| Template               | `POST` | /api/v1/template/meter                   | Get metering point mass import templates                             | Deployed   |
| Meter Data             | `POST` | /api/v1/meter-data                       | Create or update meter reading data                                  | Deployed   |
| Authorization          | `POST` | /api/v1/authorization                    | Create user authorization                                            | Deployed   |
| User Rights            | `POST` | /api/v1/user/rights/search               | Get user rights                                                      | Deployed   |
| User role types        | `GET`  | /api/v1/user-role-type                   | Get user role types                                                  | Deployed   |
| User market roles      | `GET`  | /api/v1/user/market-roles                | Get market roles of user                                             | Deployed   |
| Network Bill           | `POST` | /api/v1/network-bill                     | Create or update network bill data                                   | 2024.01.18 |
| Network Bill           | `POST` | /api/v1/network-bill/search              | Find network bill data                                               | 2024.01.18 |
| Meter Data             | `POST` | /api/v1/meter-data/export                | Export meter data                                                    | 2024.01.18 |
| Joint Invoice          | `POST` | /api/v1/joint-invoice                    | Create a joint invoice                                               | 2024.01.18 |
| Joint Invoice          | `POST` | /api/v1/joint-invoice/search             | Find a joint invoice                                                 | 2024.01.18 |
| Joint Invoice          | `POST` | /api/v1/joint-invoice/download           | Download a joint invoice                                             | 2024.01.18 |
| Customer Authorization | `POST` | /api/v1/customer-authorization/search    | Search for authorizations given by the Customer in the Client Portal | 2024.01.18 |
| Connection State       | `POST` | /api/v1/connection-state/search          | Find connection states                                               | 2024.01.31 |
| Connection State       | `POST` | /api/v1/connection-state/message         | Create connection state message                                      | 2024.01.31 |
| Connection State       | `POST` | /api/v1/connection-state/message-history | Find connection state message history                                | 2024.01.31 |
| Connection State       | `POST` | /api/v1/connection-state/initiate        | Initiate connection state change                                     | 2024.01.31 |
| Meter Data             | `POST` | /api/v1/meter-data/status                | Find meter data processing status                                    | 2024.01.31 |
| Meter Data             | `POST` | /api/v1/meter-data/search                | Find meter data                                                      | 2024.01.31 |
| Meter Data             | `POST` | /api/v1/meter-data/import                | Bulk import of metering data                                         | 2024.01.31 |
| Agreement              | `POST` | /api/v1/agreement/search/meter           | Find agreements by Metering Point                                    | 2024.01.31 |
| Authorization          | `POST` | /api/v1/authorization/search             | Get user authorizations by market role                               | 2024.01.31 |
| Authorization          | `POST` | /api/v1/authorization/delete             | Delete user authorization                                            | 2024.01.31 |
| Data Distribution      | `POST` | /api/v1/data-distribution/search         | Returns changes of different entities based on search params         | 2024.01.31 |
| Customer               | `PUT`  | /api/v1/customer                         | Update customer with metadata                                        | 2024.02.13 |
| Customer               | `POST` | /api/v1/customer                         | Create customer with metadata                                        | 2024.02.13 |
| Customer               | `POST` | /api/v1/customer/search                  | Find a customer by identity                                          | 2024.02.13 |
| Technical User         | `POST` | /api/v1/idr/technical-user               | Create technical user                                                | 2024.02.13 |
| Technical User         | `PUT`  | /api/v1/idr/technical-user               | Invalidate technical user                                            | 2024.02.13 |
| Technical User         | `POST` | /api/v1/idr/technical-user/search        | Find technical users                                                 | 2024.02.13 |
| Technical User         | `POST` | /api/v1/idr/technical-user/role          | List technical user roles                                            | 2024.02.13 |
| Metering Point         | `PUT`  | /api/v1/meter                            | Update Metering Point's metadata                                     | 2024.02.13 |
| Metering Point         | `POST` | /api/v1/meter                            | Create Metering Point with metadata                                  | 2024.02.13 |
| Metering Point         | `POST` | /api/v1/meter/search                     | Find a Metering Point by attributes                                  | 2024.02.13 |
| Metering Point         | `POST` | /api/v1/meter/search/customer            | Find a Metering Point by Customer EIC                                | 2024.02.13 |
| Metering Point         | `POST` | /api/v1/meter/search/border              | Get border Metering Points by customer                               | 2024.02.13 |
| Metering Point         | `POST` | /api/v1/meter/import                     | Mass import Metering Points with template                            | 2024.02.13 |
| Metering Point         | `POST` | /api/v1/meter/export                     | Export Metering Points by attributes                                 | 2024.02.13 |
| Balance State          | `POST` | /api/v1/balance-state/search             | Get balance state                                                    | 2024.03.12 |
| Customer Overview      | `POST` | /api/v1/customer/search/representative   | Find Estonian Business Registry representations of Customer          | 2024.03.12 |
| Customer Overview      | `POST` | /api/v1/customer/search/agreement        | Search Customer agreements                                           | 2024.03.12 |
| Customer Overview      | `POST` | /api/v1/customer/search/meter            | Search Customer's Metering Points                                    | 2024.03.12 |
| Reports                | `POST` | /api/v1/report/export/json               | Download report in JSON format                                       | 2024.03.31 |
| Reports                | `POST` | /api/v1/report/export/excel              | Download report in Excel format                                      | 2024.03.31 |
| Reports                | `POST` | /api/v1/report/search                    | Find reports                                                         | 2024.03.31 |
| Joint Invoice          | `PUT`  | /api/v1/joint-invoice                    | Update a forwarded invoice                                           | 2024.05.15 |
| Provider Management    | `PUT`  | /api/v1/identity                         | Update Identity                                                      | 2024.05.15 |
| Provider Management    | `POST` | /api/v1/identity                         | Create Identity                                                      | 2024.05.15 |
| Provider Management    | `POST` | /api/v1/provider                         | Create Provider                                                      | 2024.05.15 |
| Provider Management    | `PUT`  | /api/v1/provider                         | Update Provider                                                      | 2024.05.15 |
| Provider Management    | `POST` | /api/v1/provider/search                  | Search providers                                                     | 2024.05.15 |
| Provider Management    | `POST` | /api/v1/market-role/search               | Get market roles                                                     | 2024.05.15 |
| Provider Management    | `PUT`  | /api/v1/provider/market-role             | Update Market Role for Market Participant                            | 2024.05.15 |
| Provider Management    | `POST` | /api/v1/provider/market-role             | Create Market Role for Market Participant                            | 2024.05.15 |
| Provider Management    | `POST` | /api/v1/provider/market-role/search      | Get Market Role for Market Participant                               | 2024.05.15 |
| Provider Management    | `POST` | /api/v1/provider/eic-range               | Get a list of unused EIC-s from range                                | 2024.05.15 |
