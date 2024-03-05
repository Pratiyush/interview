**Technical Tasks**

**Task 1: Fraud Detection Method Implementation**

- Implement the `isFraud` method in `com.fiserv.interviews.challenge.service.FraudService` to evaluate transactions based on:
  1. The transaction amount should not exceed 999 units.
  2. The transaction's store name should not match any name on the blacklist, considering case-insensitive matches like "BlOcK", "TEST", or "TeSt".

- Update the corresponding test case to reflect these changes.

**Task 2: Method Integration and Testing**

- Integrate the `isFraud` method within `com.fiserv.interviews.challenge.service.TransactionalService.process(TransactionVo)`.

- Test the integration using the provided `curl` command:
  ```
  curl --silent --location 'http://localhost:9099/transaction' \
  --header 'Content-Type: application/json' \
  --data '{
    "transactionId": "TX01",
    "amount": 999,
    "storeID": "TeSt TeSt",
    "time": "2023-12-03T10:15:30.00Z"
  }'
  ```

**Task 3: Implement Controller Method for Transaction Retrieval**

- Implement a method in the controller to fetch all transactions. Utilize the given method `getTransactions()` for obtaining the list of transactions.

  **Sample Method for Getting Transactions:**

  ```java
  private static List<TransactionView> getTransactions() {
      List<TransactionView> transactions = new ArrayList<>();

      // Sample transaction 1
      transactions.add(new TransactionView()
              .transactionId("TXN1001")
              .storeID("Store A")
              .amount(250.00)
              .time(OffsetDateTime.now().minusDays(1))
              .result(TransactionView.ResultEnum.APPROVED)
              .message("Successfully processed."));

      // Sample transaction 2
      transactions.add(new TransactionView()
              .transactionId("TXN1002")
              .storeID("Store B")
              .amount(1000.00)
              .time(OffsetDateTime.now().minusDays(2))
              .result(TransactionView.ResultEnum.DECLINED)
              .message("Transaction amount exceeds the permitted limit."));

      // Sample transaction 3
      transactions.add(new TransactionView()
              .transactionId("TXN1003")
              .storeID("Blocked Store")
              .amount(50.00)
              .time(OffsetDateTime.now().minusDays(3))
              .result(TransactionView.ResultEnum.FRAUD)
              .message("Store is on the blacklist."));

      // Sample transaction 4
      transactions.add(new TransactionView()
              .transactionId("TXN1004")
              .storeID("Store C")
              .amount(500.00)
              .time(OffsetDateTime.now().minusHours(10))
              .result(TransactionView.ResultEnum.APPROVED)
              .message("Transaction approved without issues."));

      // Sample transaction 5
      transactions.add(new TransactionView()
              .transactionId("TXN1005")
              .storeID("Store D")
              .amount(750.00)
              .time(OffsetDateTime.now().minusWeeks(1))
              .result(TransactionView.ResultEnum.DECLINED)
              .message("Customer account flagged for review."));

      return transactions;
  }
  ```

- Verify the implementation with the `curl` command:
  ```
  curl --silent --location 'http://localhost:9099/transactions'
  ```

This task focuses on extending the application's functionality to include an endpoint for retrieving transaction data, showcasing the candidate's ability to integrate existing logic into new API functionalities.
