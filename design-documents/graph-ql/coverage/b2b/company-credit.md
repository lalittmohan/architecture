# Queries

```graphql

###### Begin: Extending existing types ######
type Company {
    credit: CompanyCredit! @doc(description: "Company credit balance")
    credit_history(filter: CompanyCreditHistoryFilterInput, pageSize: Int = 20, currentPage: Int = 1): CompanyCreditHistory! @doc(description: "Company credit operations history")
}
###### End: Extending existing types ######


###### Begin: Defining new types ######
type CompanyCreditHistory {
    items: [CompanyCreditOperation]! @doc(description: "An array of company credit operations")
    page_info: SearchResultPageInfo @doc(description: "Metadata for pagination rendering")
    total_count: Int! @doc(description: "The number of the company credit operations matching the specified filter")
}

type CompanyCreditOperation {
    uid: ID!  @doc(description: "Unique identifier") # id of the log entry
    date: String! @doc(description: "The date of the company credit operation")
    type: CompanyCreditOperationType! @doc(description: "The type of the company credit operation")
    amount: Money! @doc(description: "The amount fo the company credit operation")
    balance: CompanyCredit! @doc(description: "Credit balance after the company credit operation")
    custom_reference_number: String @doc(description: "Custom reference number associated with the company credit operation")
    updated_by: CompanyCreditOperationUser! @doc(description: "The user submitting the company credit operation")
}

type CompanyCreditOperationUser {
    name: String! @doc(description: "The name of the user submitting the company credit operation")
    type: CompanyCreditOperationUserType! @doc(description: "The type of the user submitting the company credit operation")
}

type CompanyCredit {
    outstanding_balance: Money! @doc(description: "Outstanding company credit")
    available_credit: Money! @doc(description: "Available company credit")
    credit_limit: Money! @doc(description: "Company credit limit")
}

enum CompanyCreditOperationType {
    ALLOCATION
    UPDATE
    PURCHASE
    REIMBURSEMENT
    REFUND
    REVERT
}

enum CompanyCreditOperationUserType {
    CUSTOMER
    ADMIN
}

input CompanyCreditHistoryFilterInput {
    operation_type: CompanyCreditOperationType @doc(description: "Enum filter by the type of the company credit operation")
    custom_reference_number: String @doc(description: "Free text filter by the custom reference number associated with the company credit operation")
    updated_by: String @doc(description: "Free text filter by the name of the person submitting the company credit operation")
}
###### End: Defining new types ######

```


