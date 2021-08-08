# Test-Automation-Best-Practices
Every test we write will include selectors for elements. To save ourselves a lot of headaches, we should write selectors that are resilient to changes.

Often times we see users run into problems targeting their elements because:
* Our application may use dynamic classes or ID's that change
* Our selectors break from development changes to CSS styles or JS behaviour

To avoid both of these problems:
1. Let’s not target elements based on CSS attributes such as id, class, tag
2. Let’s not target elements that may change their textContent
3. We can use data-* attributes to provide context to our selectors and isolate them from CSS or JS changes.
    1. Add data-* attributes to make it easier to target elements (Add data-test attribute to components)
    2. Value for data-test attribute can be like <ElementType>-<LabelForElement> 

For Example: 
<button
  id="main"
  class="btn btn-large"
  name="submission"
  data-test=“button-submit" >
  Submit
</button>

Cypress:
1. cy.get('[<attribute_name>=“<value>”]’).click() 
    1. cy.get('[data-test=submit]').click() 

Selenium:
Can find element using css selector or xpath: 
1. @FindBy(css=“element_name[<attribute_name>='<value>’]”) 
    1. @FindBy(css=“button[data-test=‘button-submit’]”)
2. @FindBy(xpath =“//element[@attribute='value’]”)
    1. @FindBy(xpath=“//button[@data-test=‘button-submit’]”)

Stage 1 : 
1. Is data-test attribute name is final or should it be something else ?
2. Adding data-test to
    1. All new component
    2. Only those components which are getting edited as part of BAU stories 
        1. Will it break any existing test/ code by adding extra attribute and not removing anything from existing.
