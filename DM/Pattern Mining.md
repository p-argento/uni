# Market Basket Analysis (MBA)
Given a set of transactions where is transaction is a set of items.
The goal is to find groups of items frequently bought together.
It is an actionable insight. The seller can sell items in a single package. 

# Association Rules
Express how product/services relate to each other and tend to group together.
"If a customer purchases diapers then will also purchase beer"
Rule form: “Body → Ηead \[support, confidence]”.
buys(x, “diapers”) → buys(x, “beers”) \[0.5%, 60%]
Body/Head/Antecedent $X\rightarrow Y$ Head/Tail/Consequent

Rules can be
1. useful
2. trivial
3. unexplicable

chatgpt
> Association rule mining, a specific type of pattern mining, involves finding rules that describe how the presence of certain items in a dataset implies the presence of other items. It specifically aims to find relationships between variables in the form of "if-then" rules, typically using measures like support and confidence to evaluate these rules.
# Apriori