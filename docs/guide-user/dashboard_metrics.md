# Dashboard Metrics Explained

The Dashboard module offers insights into payment distribution, reach, and process completion for each business area but also a Global dasboard is available with all the countries wher Hope is implemented.

The data generally includes payments associated with Payment Plans released (having statuses "ACCEPTED" or "FINISHED"), and excludes individual payments with statuses like "Transaction Erroneous", "Not Distributed", "Force failed", or "Manually Cancelled".

---

## 1. In local currency

*   **Description**: This metric shows the total monetary value of payments considered "successful", displayed in the original currency of the transactions (e.g., AFN, BIF, KSH). Only available for the country dashboard, not present in the Global one.
*   **Calculation**: Sum of payment amounts (`delivered_quantity` or `entitlement_quantity` if delivery info isn't available) for all payments with statuses: "Distribution Successful", "Partially Distributed", "Pending", "Transaction Successful".
*   **Source Fields**: `total_delivered_quantity` (from API response, derived from `Payment.delivered_quantity` or `Payment.entitlement_quantity`).
*   **Frontend Logic**: Summed in `updateTopMetrics` function (`successfulPaymentsGroup.sum`).

---

## 2. Total Amount Paid (USD)

*   **Description**: This metric shows the total monetary value of "successful" payments, converted to US Dollars (USD). This provides a standardized way to compare value across different countries or programs.
*   **Calculation**: Sum of USD-equivalent payment amounts (`delivered_quantity_usd` or `entitlement_quantity_usd`) for all payments with statuses: "Distribution Successful", "Partially Distributed", "Pending", "Transaction Successful".
*   **Source Fields**: `total_delivered_quantity_usd` (from API response, derived from `Payment.delivered_quantity_usd` or `Payment.entitlement_quantity_usd`).
*   **Frontend Logic**: Summed in `updateTopMetrics` function (`successfulPaymentsGroupUSD.sum`).

---

## 3. Number of Payments

*   **Description**: This represents the total count of individual payment records included in the current view after applying filters (like year, country, program, etc.).
*   **Calculation**: A simple count of all payment records fetched for the dashboard after initial backend filtering (excluding erroneous/cancelled statuses).
*   **Source Fields**: `payments` (from API response, representing the count of payment records in each aggregated group).
*   **Frontend Logic**: Summed in `updateTopMetrics` function (`totalPaymentsCount`).

---

## 4. Outstanding Payment (USD)

*   **Description**: This metric shows the total monetary value (in USD) of payments that have been sent to the Financial Service Provider (FSP) or Payment Gateway but are not yet confirmed as successfully distributed or failed.
*   **Calculation**: Sum of USD-equivalent payment amounts (`delivered_quantity_usd` or `entitlement_quantity_usd`) for payments with statuses: "Sent to Payment Gateway", "Sent to FSP".
*   **Source Fields**: `total_delivered_quantity_usd` (from API response).
*   **Frontend Logic**: Summed in `updateTopMetrics` function (`pendingPaymentsGroupUSD.sum`), filtering for specific pending statuses.

---

## 5. Households Reached

*   **Description**: The total count of unique households that have received at least one payment included in the current dashboard view.
*   **Calculation**: Counts the distinct households associated with the displayed payments. This aggregation happens in the backend service (`DashboardDataCache` / `DashboardGlobalDataCache`) by tracking unique `household_id` values.
*   **Source Fields**: `households` (from API response, representing the count of unique households in each aggregated group).
*   **Frontend Logic**: Summed in `updateTopMetrics` function (`householdsReached`).

---

## 6. Individuals Reached

*   **Description**: The total number of individuals belonging to the unique households reached.
*   **Calculation**: Sum of the `size` field for all unique households associated with the displayed payments. Calculated in the backend service by fetching household data (`_get_household_data`) and summing the sizes.
*   **Source Fields**: `individuals` (from API response, derived from `Household.size`).
*   **Frontend Logic**: Summed in `updateTopMetrics` function (`individualsReached`).

---

## 7. Children Reached

*   **Description**: The total number of children (typically individuals under 18) belonging to the unique households reached.
*   **Calculation**: Sum of the `children_count` field for all unique households associated with the displayed payments. Calculated in the backend service.
*   **Source Fields**: `children_counts` (from API response, derived from `Household.children_count`).
*   **Frontend Logic**: Summed in `updateTopMetrics` function (`childrenReached`).

---

## 8. PWD Reached

*   **Description**: The total number of Persons with Disabilities (PWD) belonging to the unique households reached.
*   **Calculation**: Sum of the calculated PWD count (`pwd_count_calc`) for all unique households associated with the displayed payments. The `pwd_count_calc` is derived in the backend by summing various disability count fields across age/gender groups within the `Household` model (`get_pwd_count_expression`).
*   **Source Fields**: `pwd_counts` (from API response, derived from the calculated PWD count per household).
*   **Frontend Logic**: Summed in `updateTopMetrics` function (`pwdReached`).

---

## 9. Reconciliation (%)

*   **Description**: This percentage indicates the proportion of displayed payments that are *not* in a "Pending" status. It reflects how many payments have moved beyond an initial pending state towards a final (successful or failed) status.
*   **Calculation**: `(Number of payments with status !== 'Pending' / Total number of payments) * 100`.
*   **Source Fields**: `status` (from API response).
*   **Frontend Logic**: Calculated in `updateTopMetrics` function (`reconciliationPercentage`).

---

## 10. Verification (%)

*   **Description**: This percentage represents the proportion of Payment Plans (associated with the displayed payments) that have been fully verified, meaning their corresponding `PaymentVerificationSummary` status is "FINISHED".
*   **Calculation**: `(Sum of finished_payment_plans / Sum of total_payment_plans) * 100`. The counts of finished and total plans are calculated in the backend service (`_get_payment_plan_counts`) based on the status of related `PaymentVerificationSummary` records and aggregated per group.
*   **Source Fields**: `finished_payment_plans`, `total_payment_plans` (from API response).
*   **Frontend Logic**: Calculated in `updateTopMetrics` function (`verificationPercentage`).

---
