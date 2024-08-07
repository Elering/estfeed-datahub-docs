# Andmevahetusliidese veakoodid

## Sisukord

- [Andmevahetusliidese veakoodid](#andmevahetusliidese-veakoodid)
  - [Sisukord](#sisukord)
  - [Sissejuhatus](#sissejuhatus)
  - [/agreement](#agreement)
  - [/authentication](#authentication)
  - [/connection-state](#connection-state)
  - [/customer](#customer)
  - [/data-distribution](#data-distribution)
  - [/joint-invoice](#joint-invoice)
  - [/meter-data](#meter-data)
  - [/meter](#meter)
  - [/network-bill](#network-bill)
  - [/technical-user](#technical-user)
  - [/report](#report)
  - [/authorization](#authorization)
  - [Common codes](#common-codes)

## Sissejuhatus

Veaolukorra tekkimisel vastab Andmeladu sõnumile veakoodiga. Näide:

```json
{
  "id": "8e11eab4-e56c-431a-9e93-3dded6bd7368",
  "cause": {
    "message": "commodityType can be ELECTRICITY or NATURAL_GAS",
    "code": "opp.error.validation.invalid-enum",
    "traceId": "b59c423e058940c4abb27df5c83c97bc",
    "args": [
      "commodityType",
      "ELECTRICITY or NATURAL_GAS"
    ]
  }
}
```

Veasõnumitel on alati sama struktuur:

- `message` on inimkeelde tõlgitud veateade
- `code` on tehniline veakood, mida liidestunud süsteem saab kasutada veaolukorra automaatsel käitlemisel
- `traceId` on unikaalne ID, mida Eleringi tehniline meeskond saab kasutada vea põhjuse välja selgitamiseks
- `args` sisaldab täiendavat informatsiooni. Võib olla tühi.

> [!NOTE]
> Käesolevas dokumendis on katmata veakoodid, mis algavad teise prefiksiga, nagu näiteks "mpd" ja "mpm". Need veakoodid on ajutised ning korrastatakse arenduste käigus

## /agreement

Validatsiooni veakoodid:

- `opp.error.validation.agreement-attributes-required-one-of`: 'One of the following properties is required: agreementId, meterEic, customerEic, serviceProviderEic'

Äriloogika veakoodid:

- `opp.error.business.agreement-list-cannot-be-retrieved`: 'Agreement list can not be retrieved'
- `opp.error.business.sender-and-service-provider-mismatch-error`: 'Sender and Service Provider must be the same'
- `opp.error.business.sender-and-customer-mismatch-error`: 'Sender and Customer must be the same'
- `opp.error.business.service-provider-type-error`: 'Type of Service Provider is incorrect'
- `opp.error.business.border-supply-cannot-be-created-modified-or-deleted-manually`: 'Border Supply agreement cannot be created, modified or deleted manually'
- `opp.error.business.general-service-cannot-be-created-modified-or-deleted-manually`: 'General Service agreement cannot be created, modified or deleted manually'
- `opp.error.business.agreement-type-cannot-be-processed`: 'Agreement type cannot be processed'
- `opp.error.business.agreement-cannot-be-found`: 'Agreement cannot be found'
- `opp.error.business.customer-type-error`: 'Type of Customer is incorrect'
- `opp.error.business.commodity-type-mismatch-error`: 'Market participant can only create entities with own commodity type'
- `opp.error.business.sender-type-error`: 'Type of Sender is incorrect'

## /authentication

Autentimise veakoodid:

- `opp.error.technical.authentication`: 'An error has occurred during authentication process'
- `opp.error.technical.ip-address-not-allowed`: 'IP address is not allowed'
- `opp.error.technical.jwt-format`: 'Incorrect JWT format'
- `opp.error.technical.jwt-processing`: 'An error occurred while processing the contents of the JWT token'
- `opp.error.technical.unprocessable-market-participant-context`: 'An error occurred while processing marketParticipantContext'

## /connection-state

Validatsiooni veakoodid:

- `opp.error.validation.only-one-message-can-be-sent-for-connection-state-header`: 'Only one message can be sent for connection state header'
- `opp.error.validation.connection-state-participant-should-match-market-participant-identification`: 'Participant should match with market participant identification'
- `opp.error.validation.connection-state-preferred-date-can-be-sent-by-os-only`: 'Preferred date can be sent by Open Supplier only'
- `opp.error.validation.connection-state-estimated-date-can-be-sent-by-go-and-iso-only`: 'Estimated date can be sent by Grid Operator or Closed Distribution Network'
- `opp.error.validation.connection-state-preferred-date-cannot-be-in-past`: 'Preferred date cannot be in the past'
- `opp.error.validation.connection-state-estimated-date-cannot-be-in-past`: 'Estimated date cannot be in the past'

Äriloogika veakoodid:

- `opp.error.business.provided-connection-state-cannot-be-initiated`: 'The provided connection state cannot be initiated.'
- `opp.error.business.connection-state-search-with-invalid-role`: 'Connection State search with invalid role.'
- `opp.error.business.connection-state-search-role-eic-mismatch`: 'senderEic or receiverEic must match the marketParticipantIdentification'
- `opp.error.business.connection-state-history-market-participant-must-be-sender-or-receiver`: 'Market participant must be the sender or the receiver of the message header'
- `opp.error.business.redundant-connection-state-initialization`: 'Initialization with the same customer, meter and receiver is not possible'
- `opp.error.business.connection-state-header-not-exists`: 'Connection state header does not exist'
- `opp.error.business.connection-state-reason-must-be-provided-in-case-of-refused-state`: 'Reason must be provided in case of refused state'
- `opp.error.business.connection-state-message-next-state-is-not-allowed`: 'Next state sent for connection state message is not allowed'
- `opp.error.business.connection-state-process-terminated`: 'Connection state process is terminated. No further message can be received'
- `opp.error.business.connection-state-participant-must-be-sender-or-receiver`: 'Participant must be the sender or the receiver of the connection state'
- `opp.error.business.mismatched-initiation-reason-and-state`: 'The provided connection state cannot be initiated with the given reason.'
- `opp.error.business.service-provider-role-and-initiation-mismatch`: 'The given service provider role cannot initiate connection state change.'
- `opp.error.business.missing-agreement-between-go-and-os`: 'Open Supplier and Grid Operator has no valid agreement.'
- `opp.error.business.missing-agreement-between-os-and-cust`: 'Open Supplier and Customer has no valid agreement.'
- `opp.error.business.missing-agreement-between-go-and-cust`: 'Grid Operator and Customer has no valid agreement.'

## /customer

Äriloogika veakoodid:

- `opp.error.business.eic-has-no-extension`: 'Extension cannot be assigned to EIC code'
- `opp.error.business.name-has-no-extension`: 'Extension cannot be assigned to Name'
- `opp.error.business.customer-type-identity-type-mismatch`: 'This Customer type cannot have the given Identity type'
- `opp.error.business.customer-type-metadata-type-mismatch`: 'This Customer type cannot have the given Metadata type'
- `opp.error.business.internal-id-resolve-error`: 'Internal ID of the Service Provider cannot be resolved.'
- `opp.error.business.search-by-name-is-not-supported-for-these-customers`: 'Customer search by name is not supported by the given customer types'
- `opp.error.business.customer-metadata-not-found`: 'Customer metadata not found'
- `opp.error.business.country-extension-required`: 'Country extension is required for identity types: PERSONAL_ID, COMPANY_ID, DOCUMENT_ID, EMBASSY_ID'
- `opp.error.business.personal-id-and-document-id-cannot-be-included-in-one-request`: 'PERSONAL_ID and DOCUMENT_ID cannot be included in one request'
- `opp.error.business.eic-cannot-be-created-via-request`: 'EIC cannot be created via request'
- `opp.error.business.no-duplicate-country-extensions-allowed`: 'Duplicates of country extension is not allowed for the same identity'
- `opp.error.business.country-code-must-be-filled`: 'For COUNTRY extension, country code must be filled'
- `opp.error.business.market-participant-cannot-update-customer`: 'Market participant cannot update customer due to missing agreement or insufficient role'
- `opp.error.business.already-exists`: '{0} value with {1} business object type and {2} identity type already exists'

## /data-distribution

Validatsiooni veakoodid:

- `dd.error.validation.data-distribution-created-time-period-max-one-day`: 'Created time period maximum value can be one day'
- `dd.error.validation.data-distribution-created-time-period-max-one-hour`: 'Created time period maximum value can be one hour'
- `dd.error.validation.data-distribution-id-range-or-time-interval-is-required`: 'Id range or created time period is required'
- `dd.error.validation.data-distribution-id-from-can-not-be-bigger-than-id-to`: 'Id from can not be greater than id to'
- `dd.error.validation.data-distribution-id-can-not-be-negative-number`: 'Id can not be a negative number'
- `dd.error.validation.data-distribution-id-range-exceeds-max-number`: 'Id range exceeds maximum number'
- `dd.error.validation.data-distribution-provide-from-and-to-params-together`: 'From and To parameters must be provided together'

Äriloogika veakoodid:

- `dd.error.business.overlapping-agreements`: 'Agreements have overlapping validity dates for the same meter'

## /joint-invoice

Validatsiooni veakoodid:

- `opp.error.validation.joint-invoice-headers-and-invoice-files-size-must-be-equal`: 'The joint invoice headers and invoice file must have the same number of elements'
- `opp.error.validation.joint-invoice-header-file-name-must-be-unique`: 'The file name must be unique in the joint invoice headers'
- `opp.error.validation.joint-invoice-file-name-must-match-with-the-file-name-from-the-header`: 'The file name form the header must be match with the file name'
- `opp.error.validation.joint-invoice-market-participant-and-sender-mismatch`: 'Market participant and Sender do not match'

Äriloogika veakoodid:

- `opp.error.business.joint-invoice-missing-file`: 'Invoice file is required'
- `opp.error.business.joint-invoice-agreement-coverage-error`: 'The interval of the Joint Invoice is not covered by agreements'
- `opp.error.business.find-joint-invoice-interval-too-long`: 'The interval of the query is too long'
- `opp.error.business.download-joint-invoice-not-found`: 'The searched joint invoice is not found'
- `opp.error.business.joint-invoice-incorrect-market-participant-role`: 'Joint invoice can be created by the following market roles: Grid operator, Closed distribution network'
- `opp.error.business.joint-invoice-search-incorrect-market-participant-role`: 'Joint invoice can be searched by the following market roles: Grid operator, Closed distribution network, Open supplier'
- `opp.error.business.joint-invoice-already-exists`: 'Joint invoice already exists for the given parameters'
- `opp.error.business.joint-invoice-not-exists`: 'Joint invoice not exists for the given parameters, cannot be updated'

## /meter-data

Validatsiooni veakoodid:

- `opp.error.validation.meter-data-status-interval-max-length`: 'Meter data status search interval cannot be longer than 30 days'
- `opp.error.validation.too-many-decimals`: 'Number of decimals can not be more than 3'
- `opp.error.validation.field-value-cannot-be-negative`: 'Number cannot be smaller than zero'

Äriloogika veakoodid:

- `opp.error.business.legal-consent-with-incorrect-role`: 'Only Market Participants with Open Supplier or Aggregator role can view Metering Data by accepting legal consent'
- `opp.error.business.legal-consent-with-incorrect-customer-type`: 'Only Legal Person or Organization can view Metering Data by accepting legal consent'
- `opp.error.business.meter-data-cannot-be-retrieved`: 'Meter data cannot be retrieved'
- `opp.error.business.market-participant-mismatch-error`: 'Only meterOwnerInternalId of Metering Point can send measurement data to Metering Point'
- `opp.error.business.metering-data-with-this-commodity-type-cannot-be-created-with-this-market-participant-role`: 'Metering Data with this commodity type cannot be created with this Market Participant Role.'
- `opp.error.business.wrong-measurement-value`: 'Must be greater than or equal to 0 and less than 4 decimals.'
- `opp.error.business.metering-data-is-duplicated`: 'Metering data is duplicated'
- `opp.error.business.wrong-resolution`: 'Resolution of metering data is incorrect'
- `opp.error.business.timestamp-of-hourly-resolution-wrong-format`: 'Timestamp of hourly resolution can have the following format: yyyy-MM-ddTHH:00:00Z'
- `opp.error.business.timestamp-of-quarterly-resolution-wrong-format`: 'Timestamp of quarterly resolution can have the following format: yyyy-MM-ddTHH:00:00Z, yyyy-MM-ddTHH:15:00Z, yyyy-MM-ddTHH:30:00Z,yyyy-MM-ddTHH:45:00Z'
- `opp.error.business.timestamp-of-daily-resolution-wrong-format`: 'Timestamp of daily resolution can have the following format: yyyy-MM-ddTHH:07:00Z or yyyy-MM-ddTHH:00:00Z based on the selected commodity type'

## /meter

Validatsiooni veakoodid:

- `opp.error.validation.metering-point-must-have-minimum-one-characteristic`: 'Metering point must have minimum of one characteristic'
- `opp.error.validation.metering-point-can-only-have-natural-gas-or-electricity-characteristics`: 'Can only have either natural gas or electricity characteristics with this metering point type'
- `opp.error.validation.metering-point-can-only-have-aggregator-characteristics`: 'Can only have aggregator characteristics with this metering point type'
- `opp.error.validation.incorrect-owner-market-role-type`: 'Type of Owner Market Role is incorrect'

Äriloogika veakoodid:

- `opp.error.business.metering-point-external-id-resolve-error`: 'External ID of the meter point cannot be resolved'
- `opp.error.business.metering-point-not-exists`: 'Metering point does not exist'
- `opp.error.business.invalid-substation`: 'Substation does not exist'
- `opp.error.business.invalid-parent`: 'Parent metering point does not exist'
- `opp.error.business.incorrect-characteristics-type`: 'Changing the type of characteristics is not allowed'
- `opp.error.business.multiple-characteristics-assignment`: 'Metering point can only have one characteristic'
- `opp.error.business.metering-point-type-cannot-be-updated`: 'Metering point type cannot be updated, must be null'
- `opp.error.business.metering-point-cannot-be-found`: 'Metering Point cannot be found'
- `opp.error.business.metering-point-is-duplicated`: 'Metering Point in excel was duplicated'
- `opp.error.business.market-participant-has-no-access-to-meter-point`: 'Market participant has no access to meter point'
- `opp.error.business.border-point-cannot-be-found`: 'Border Point cannot be found'
- `opp.error.business.eic-syntax-evaluation-error`: 'Eic syntax cannot be evaluated'
- `opp.error.business.eic-syntax-error`: 'Eic syntax is incorrect'
- `opp.error.business.eic-range-evaluation-error`: 'Eic range cannot be evaluated'
- `opp.error.business.eic-range-error`: 'Eic code is not in range of Market Participant'
- `opp.error.business.incorrect-market-participant-role`: 'Metering Point cannot be created or updated with this Market Participant Role Type'
- `opp.error.business.source-type-error`: 'Market Participant with this role cannot access Metering Point with some of the requested source types'
- `opp.error.business.legal-consent-is-not-required-for-the-given-customer`: 'Legal consent can only be given, when the customer''s business object type is legal person or organization'

## /network-bill

Validatsiooni veakoodid:

- `opp.error.validation.invalid-measurement-type`: 'Invalid measurement type'
- `opp.error.validation.duplicate-measurement-unit-by-direction`: 'Duplicate measurement units for direction {0}'
- `opp.error.validation.missing-agreement-for-period`: 'Missing {1} agreement for period {2} - {3}'
- `opp.error.validation.period-is-not-covered-by-agreement`: 'The given Period {2} - {3} is not covered by {1} agreement'

Äriloogika veakoodid:

- `opp.error.business.network-bill-search-with-insufficient-role`: 'Searching for network bill is impossible with the given role.'

## /technical-user

Äriloogika veakoodid:

- `opp.error.business.technical-user-number-exceeds-maximum`: 'Number of the technical users by market participant exceeds the maximum number'
- `opp.error.business.technical-user-suffix-needs-to-be-unique`: 'Suffix must be unique by market participants'

Tehnilised veakoodid:

- `opp.error.technical.failed-to-create-client-in-keycloak`: "Failed to create new client in keycloak. For further details please check the logs"

## /report

Validatsiooni veakoodid:

- `opp.error.validation.greater-end-month-offset-than-start`: 'endMonthOffset cannot be greater than startMonthOffset'
- `opp.error.validation.commodity-type-not-supported`: 'Commodity type not supported'
- `opp.error.validation.report-type-not-supported`: 'Report type not supported'

Äriloogika veakoodid:

- `opp.error.business.report-header-not-found`: 'Report header not found'
- `opp.error.business.service-provider-market-role-does-not-exist`: 'Necessary market roles for service providers not found'

## /authorization

Validatsiooni veakoodid:

- `authz.error.validation.missing.%s`: 'Missing from request: %s'
- `authz.error.validation.max-length.%s`: '%s cannot be longer than %d characters'
- `authz.error.validation.invalid-enum.%s`: '%s can be %s'
- `authz.error.validation.unparseable.%s`: 'Field %s can not be parsed for value %s'
- `authz.error.validation.wrong-order.%s`: '%s cannot be after %s'
- `authz.error.validation.role-cannot-be-assigned`: 'The selected role cannot be assigned'
- `authz.error.validation.self-authorization-not-permitted`: 'Adding or removing roles to self is not permitted'

Äriloogika veakoodid:

- `authz.error.business.not-found.authorization`: 'Authorization not found'
- `authz.error.business.not-found.market-role`: 'Market role not found'
- `authz.error.business.not-found.role`: 'Role not found'
- `authz.error.business.not-found.right`: 'Right not found'
- `authz.error.business.authorization-does-not-exist`: 'Authorization does not exist'
- `authz.error.business.general.no-change`: 'No change received'
- `authz.error.business.service-provider-does-not-exist`: 'Service Provider does not exist'
- `authz.error.business.service-provider-does-not-exist-on-period`: 'Service Provider does not exist on the whole period'
- `authz.error.business.valid-from-cannot-be-in-past`: 'Authorization of a user cannot start in the past'
- `authz.error.business.invalid-validity`: 'Invalid validity period'
- `authz.error.business.user-role-cannot-be-assigned-to-service-provider-role`: 'This user role cannot be assigned to this service provider role'
- `authz.error.business.user-does-not-exist`: 'The user in this context has not been created yet'
- `authz.error.business.user-is-not-authorized-with-this-role`: 'User is not authorized with this role'
- `authz.error.business.market-role-already-exists`: 'Market Participant Role already exists'
- `authz.error.business.user-already-exist`: 'The user in this context has already been created'

Tehnilised veakoodid:

- `authz.error.technical.general`: 'An error has occurred while processing the request'
- `authz.error.technical.general.no-response`: 'No valid response from server'
- `authz.error.technical.not-found.header`: 'No header data found'

## Common codes

Validatsiooni veakoodid:

- `opp.error.validation.missing`: 'Missing from request: {0}'
- `opp.error.validation.invalid-pattern`: '{0} for value {1} must match {2}'
- `opp.error.validation.invalid-email`: '{0} must be a well-formed email address'
- `opp.error.validation.size`: '{0} with value {1} size must be between {2} and {3}'
- `opp.error.validation.too-small`: '{0} with value {1} must be greater than or equal to {2}'
- `opp.error.validation.too-big`: '{0} with value {1} must be less than or equal to {2}'
- `opp.error.validation.too-many-entries`: '{0} for value {1} must match {2}'
- `opp.error.validation.missing-field`: 'Missing field {0}'
- `opp.error.validation.invalid-enum`: '{0} can be {1}'
- `opp.error.validation.unparseable`: 'Field {0} can not be parsed for value {1}'
- `opp.error.validation.unparseable-object`: 'Object {0} can not be parsed, cause: {1}'
- `opp.error.validation.from-field-cannot-be-equal-to-or-after-to-field`: 'For {0} {1} cannot be equal or after {2}'
- `opp.error.validation.period-is-invalid`: '{0} provided by fields {1} and {2} is invalid.'
- `opp.error.validation.field-cannot-be-longer-than-x-characters`: '{0} cannot be longer than {1} characters'
- `opp.error.validation.field-value-cannot-be-negative`: '{0} cannot be smaller than zero'
- `opp.error.validation.greater-or-equal`: '{0} must be grater than or equal to {1}'
- `opp.error.validation.too-many-decimals`: '{0} has too many decimals'
- `opp.error.validation.unauthorized-user`: 'User is not authorized to initiate this request'
- `opp.error.validation.unsupported-file-format`: 'Please select a valid Excel file with the ‘.xlsx’ extension'
- `opp.error.validation.file-not-found`: 'File not found'
- `opp.error.validation.list-can-not-be-empty`: '{0} can not be empty'

Äriloogika veakoodid:

- `opp.error.business.market-participant-external-id-resolve-error`: 'External ID of the market participant cannot be resolved'
- `opp.error.business.service-provider-external-id-resolve-error`: 'External ID of the service provider cannot be resolved'
- `opp.error.business.service-provider-internal-id-resolve-error`: 'Internal ID of Service Provider cannot be resolved'
- `opp.error.business.sender-and-service-provider-mismatch-error`: 'Sender and Service Provider must be the same'
- `opp.error.business.request-commodity-type-mismatch`: 'Commodities do not match'
- `opp.error.business.customer-external-id-resolve-error`: 'External ID of customer cannot be resolved'
- `opp.error.business.customer-internal-id-resolve-error`: 'Internal ID of Customer cannot be resolved'
- `opp.error.business.user-external-id-resolve-error`: 'External ID of user cannot be resolved'
- `opp.error.business.permission-list-cannot-be-retrieved`: 'Permission list can not be retrieved'
- `opp.error.business.no-change-received`: 'No change received'
- `opp.error.business.not-found.customer-identification`: 'Identification not found'
- `opp.error.business.not-found.service-provider-identification`: 'Identification not found'
- `opp.error.business.non-complete-gps-location`: 'GPS coordinates can only be given, if both latitude and longitude are given'

Tehnilised veakoodid:

- `opp.error.technical.general`: 'An error has occurred while processing the request'
- `opp.error.technical.excel-generation-exception`:` 'Unexpected error happened during excel generation'
- `opp.error.technical.not-found.resource-file`: 'Resource file not found'
- `opp.error.technical.not-found.resource`: 'Resource not found'
- `opp.error.technical.json-processing-exception`: 'An error occurred while processing JSON'
- `opp.error.technical.no-response`: 'No valid response from server'
- `opp.error.technical.not-found.header`: 'No header data found'
- `opp.error.technical.scheduler-exception`: 'An error occurred while scheduling jobs'
- `opp.error.technical.scheduler-parameter-parse-exception`: 'An error occurred while parsing job parameters'