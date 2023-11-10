One aim of any application logic is to restrict user input to values that adhere to the business rules. For example, the application may be designed to accept values of a certain data type, but the logic determines whether or not this value is acceptable from the perspective of the business. Many applications incorporate numeric limits into their logic. This might include limits designed to manage inventory, apply budgetary restrictions, trigger phases of the supply chain, and so on.

To implement rules like this, developers need to anticipate all possible scenarios and be able to handle them into the application logic, as failure to handle a specific scenario can lead to unexpected and potentially exploitable behavior.

For example, a numeric data type might accept negative values. Consider a fund transfer between two bank accounts, the application will typically check whether the sender has sufficient funds. Although any integer is theoretically a valid input, the application might not prevent users from supplying a negative value, which could be exploited by an attacker to bypass the balance check and transfer funds in the "wrong direction". If the attacker sent -$1000 to the victim's account, this might result in them receiving $1000 from the victim instead.

When auditing an application, developers must use tools such as Burp Proxy and Repeater to try submitting unconventional values such as exceptionally low numeric inputs and abnormally long strings. They can even try unexpected data types. By observing the application's response, they must be able to try and answer the following questions:
- Are there any limits that are imposed on the data?
- What happens when you reach those limits?
- Is any transformation or normalization being performed on your input?
## Examples from PortSwigger Web Academy
![High level logic vulnerability (Video solution, Audio)](https://www.youtube.com/watch?v=FxJrvNJsi48)
![Low level logic flaw (Video solution, audio)](https://www.youtube.com/watch?v=BpAc15a5m_Q)
aa