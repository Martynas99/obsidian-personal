Functional Requirements:
- Users should be able to create a group, add/remove users from a group
- Users should be able to log expenses against a group, with a custom split against group members
- Users should be bale to see all expenses, edit their own logged expenses
- User should be able to view balance of their own and other members

Non functional requirements
- Easy to add payment methods
- Fast to see what you owe/are owed

Out of scope:
- Currencies
- UI
- Payment platform integrations

Object modelling
Group:
- Members
- Expense tracker

Member:
- name
- bank deets (maybe)

Transaction:
- value
- split_map (member -> value)

Expense tracker:
- Transaction log
- Balances

Group:
- add_member(self, Member) -> None
- remove_member(self, Member) -> None
- log_transaction(self, Member, Transaction) -> None
- get_balance(self, Member) -> float
- view_transactions(self, Member [optional]) -> list[Transaction]

Transaction:
- get_value() -> float
- get_member_value(Member) -> float

ExpenseTracker:
- add_transaction(Member, Transaction)
- show_balances() -> dict[Member -> float]
- show_balance(Member) -> float
- edit_transaction(uuid, newTransaction)
- view_transactions(Member[optional]) -> list[Transaction]

SplitStrategy(ABC):
- get_split_map(value, splits: list[Member] | dict[Member, float])

EqualSplitStrategy:
- get_split_map:
	- return value / len(splits)

PercentageSplitStrategy:
- get_split_map:
	- validate that values sum to 100
	- return {member: value * percentage / 100 for member, percentage in splits.values()}

ExactSplitStrategy:
- get_split_map:
	- validate sums to value
	- return splits
