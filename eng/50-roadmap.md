# Roadmap

## API developments

| Topic                  | Type   | Endpoint                                 | Description                                                                      | Deployment |
|------------------------|--------|------------------------------------------|----------------------------------------------------------------------------------|------------|
| Agreement              | `POST` | /api/v1/agreement                        | Create agreement                                                                 | Deployed   |
| Agreement              | `PUT`  | /api/v1/agreement                        | Update agreement                                                                 | Deployed   |
| Agreement              | `POST` | /api/v1/agreement/search                 | Find agreements                                                                  | Deployed   |
| Agreement              | `POST` | /api/v1/agreement/export                 | Export agreements by attributes                                                  | Deployed   |
| Agreement              | `POST` | /api/v1/agreement/delete                 | Delete agreement                                                                 | Deployed   |
| Template               | `POST` | /api/v1/template/meter                   | Get metering point mass import templates                                         | Deployed   |
| Meter Data             | `POST` | /api/v1/meter-data                       | Create or update meter reading data                                              | Deployed   |
| Authorization          | `POST` | /api/v1/authorization                    | Create user authorization                                                        | Deployed   |
| User Rights            | `POST` | /api/v1/user/rights/search               | Get user rights                                                                  | Deployed   |
| User role types        | `GET`  | /api/v1/user-role-type                   | Get user role types                                                              | Deployed   |
| User market roles      | `GET`  | /api/v1/user/market-roles                | Get market roles of user                                                         | Deployed   |
| Network Bill           | `POST` | /api/v1/network-bill                     | Create or update network bill data                                               | Deployed   |
| Network Bill           | `POST` | /api/v1/network-bill/search              | Find network bill data                                                           | Deployed   |
| Meter Data             | `POST` | /api/v1/meter-data/export                | Export meter data                                                                | Deployed   |
| Joint Invoice          | `POST` | /api/v1/joint-invoice                    | Create a joint invoice                                                           | Deployed   |
| Joint Invoice          | `POST` | /api/v1/joint-invoice/search             | Find a joint invoice                                                             | Deployed   |
| Joint Invoice          | `POST` | /api/v1/joint-invoice/download           | Download a joint invoice                                                         | Deployed   |
| Customer Authorization | `POST` | /api/v1/customer-authorization/search    | Search for authorizations given by the Customer in the Client Portal             | Deployed   |
| Connection State       | `POST` | /api/v1/connection-state/search          | Find connection states                                                           | Deployed   |
| Connection State       | `POST` | /api/v1/connection-state/message         | Create connection state message                                                  | Deployed   |
| Connection State       | `POST` | /api/v1/connection-state/message-history | Find connection state message history                                            | Deployed   |
| Connection State       | `POST` | /api/v1/connection-state/initiate        | Initiate connection state change                                                 | Deployed   |
| Meter Data             | `POST` | /api/v1/meter-data/status                | Find meter data processing status                                                | Deployed   |
| Meter Data             | `POST` | /api/v1/meter-data/search                | Find meter data                                                                  | Deployed   |
| Meter Data             | `POST` | /api/v1/meter-data/import                | Bulk import of metering data                                                     | Deployed   |
| Agreement              | `POST` | /api/v1/agreement/search/meter           | Find agreements by Metering Point                                                | Deployed   |
| Authorization          | `POST` | /api/v1/authorization/search             | Get user authorizations by market role                                           | Deployed   |
| Authorization          | `POST` | /api/v1/authorization/delete             | Delete user authorization                                                        | Deployed   |
| Customer               | `PUT`  | /api/v1/customer                         | Update customer with metadata                                                    | Deployed   |
| Customer               | `POST` | /api/v1/customer                         | Create customer with metadata                                                    | Deployed   |
| Customer               | `POST` | /api/v1/customer/search                  | Find a customer by identity                                                      | Deployed   |
| Technical User         | `POST` | /api/v1/idr/technical-user               | Create technical user                                                            | Deployed   |
| Technical User         | `PUT`  | /api/v1/idr/technical-user               | Invalidate technical user                                                        | Deployed   |
| Technical User         | `POST` | /api/v1/idr/technical-user/search        | Find technical users                                                             | Deployed   |
| Technical User         | `POST` | /api/v1/idr/technical-user/role          | List technical user roles                                                        | Deployed   |
| Metering Point         | `PUT`  | /api/v1/meter                            | Update Metering Point's metadata                                                 | Deployed   |
| Metering Point         | `POST` | /api/v1/meter                            | Create Metering Point with metadata                                              | Deployed   |
| Metering Point         | `POST` | /api/v1/meter/search                     | Find a Metering Point by attributes                                              | Deployed   |
| Metering Point         | `POST` | /api/v1/meter/search/customer            | Find a Metering Point by Customer EIC                                            | Deployed   |
| Metering Point         | `POST` | /api/v1/meter/search/border              | Get border Metering Points by customer                                           | Deployed   |
| Metering Point         | `POST` | /api/v1/meter/import                     | Mass import Metering Points with template                                        | Deployed   |
| Metering Point         | `POST` | /api/v1/meter/export                     | Export Metering Points by attributes                                             | Deployed   |
| Balance State          | `POST` | /api/v1/balance-settlement-point/search  | Give back the changes in Balance Settlement Points to the Balance Provider party | Deployed   |
| Metering Point         | `POST` | /api/v1/meter/eic/amount                 | Generate the requested amount of metering point EICs                             | Deployed   |
| Reports                | `POST` | /api/v1/report/export/json               | Download report in JSON format                                                   | 2024.05.20 |
| Reports                | `POST` | /api/v1/report/export/excel              | Download report in Excel format                                                  | 2024.05.20 |
| Reports                | `POST` | /api/v1/report/search                    | Find reports                                                                     | 2024.05.20 |
| Joint Invoice          | `PUT`  | /api/v1/joint-invoice                    | Update a forwarded invoice                                                       | 2024.04.22 |
| Data Distribution      | `POST` | /api/v1/data-distribution/search         | Returns changes of different entities based on search params                     | 2024.05.01 |
