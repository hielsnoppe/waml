# Web Automation Markup Language Schema

## Web Automation Markup Language
```
id: 'http://waml.automate.website/draft-0.2/base-schema#'
$schema: 'http://json-schema.org/draft-04/schema#'
title: Web Automation Markup Language
description: A simple markup language for web automation.
type: array
items:
  $ref: 'http://waml.automate.website/draft-0.2/scenario-schema#'
additionalProperties: false

```
## Scenario
```
id: 'http://waml.automate.website/draft-0.2/scenario-schema#'
$schema: 'http://json-schema.org/draft-04/schema#'
title: Scenario
description: A scenario combines a collection of tasks that must be executed together in a certain order.
type: object
properties:
  $schema:
    type: string
    description: Defines the scenario schema in a specific version.
  name:
    type: string
    description: Unique name that is used to reference a certain scenario.
  title:
    type: string
    description: Human readable scenario name.
  description:
    type: string
    description: Short summary of the overall scenario purpose.
  type:
    type: string
    description: Defines if a scenario may be executed stand-alone or only as a part of another scenario.
    enum:
      - fragment
      - doable
    default: doable
  precendence:
    type: integer
    description: Defines the particular priority of the scenario during execution of independent scenarios.
    default: -1
  timeout:
    oneOf:
      - $ref: 'http://waml.automate.website/draft-0.2/expression-schema#'
      - type: integer
    description: 'Maximal time [ms] to wait for conditions to be true.'
    default: 1000
  steps:
    type: array
    items:
      $ref: 'http://waml.automate.website/draft-0.2/step-schema#'
  if:
    $ref: 'http://waml.automate.website/draft-0.2/expression-schema#'
    description: 'If set, the scenario is only executed if the value evaluates to true'
  unless:
    $ref: 'http://waml.automate.website/draft-0.2/expression-schema#'
    description: 'If set, the scenario is only executed if the value evaluates to false'
additionalProperties: false
required:
  - name
  - steps

```
## Step
```
id: 'http://waml.automate.website/draft-0.2/step-schema#'
$schema: 'http://json-schema.org/draft-04/schema#'
title: Step
type: object
description: A step represents the smallest identifiable user action.
oneOf:
  - $ref: 'http://waml.automate.website/draft-0.2/url-command-schema#'
  - $ref: 'http://waml.automate.website/draft-0.2/include-command-schema#'
  - $ref: 'http://waml.automate.website/draft-0.2/store-command-schema#'
  - $ref: 'http://waml.automate.website/draft-0.2/ensure-command-schema#'
  - $ref: 'http://waml.automate.website/draft-0.2/click-command-schema#'
  - $ref: 'http://waml.automate.website/draft-0.2/select-command-schema#'
  - $ref: 'http://waml.automate.website/draft-0.2/enter-command-schema#'

```
## Ensure the presence of an element
```
id: 'http://waml.automate.website/draft-0.2/ensure-command-schema#'
$schema: 'http://json-schema.org/draft-04/schema#'
title: Ensure the presence of an element
description: Ensures the presence of an element using different criteria
properties:
  ensure:
    description: A CSS selector as value or a hash of conditionals.
    oneOf:
      - $ref: 'http://waml.automate.website/draft-0.2/expression-schema#'
      - $ref: 'http://waml.automate.website/draft-0.2/ensure-criteria-schema#'
additionalProperties: false

```
## Include Scenario
```
id: 'http://waml.automate.website/draft-0.2/include-command-schema#'
$schema: 'http://json-schema.org/draft-04/schema#'
title: Include Scenario
description: Includes a scenario with a certain title
properties:
  include:
    $ref: 'http://waml.automate.website/draft-0.2/expression-schema#'
    description: The title of the scenario to include
required:
  - include

```
## Select from dropdown
```
id: 'http://waml.automate.website/draft-0.2/select-command-schema#'
$schema: 'http://json-schema.org/draft-04/schema#'
title: Select from dropdown
description: Selects from dropdown by the given criteria.
properties:
  select:
    description: Criteria of the element to select.
    $ref: 'http://waml.automate.website/draft-0.2/select-criteria-schema#'
additionalProperties: false

```
## Store variable
```
id: 'http://waml.automate.website/draft-0.2/store-command-schema#'
$schema: 'http://json-schema.org/draft-04/schema#'
title: Store variable
description: Includes a scenario with a certain title
properties:
  store:
    type: object
    description: A hash of variables to be defined in the execution context.
    minProperties: 1
    $ref: null
additionalProperties: false
definitions:
  entry:
    $ref: 'http://waml.automate.website/draft-0.2/expression-schema#'

```
## Url
```
id: 'http://waml.automate.website/draft-0.2/url-command-schema#'
$schema: 'http://json-schema.org/draft-04/schema#'
title: Url
description: Navigates to a certain URL in the user agent
allOf:
  - $ref: 'http://waml.automate.website/draft-0.2/base-command-schema#'
  - properties:
      url:
        $ref: 'http://waml.automate.website/draft-0.2/expression-schema#'
        description: The url to which the navigation takes place.
    required:
      - url

```
## 
```
id: 'http://waml.automate.website/draft-0.2/base-command-schema#'
$schema: 'http://json-schema.org/draft-04/schema#'
properties:
  $schema:
    type: string
  if:
    $ref: 'http://waml.automate.website/draft-0.2/expression-schema#'
    description: 'If set, the step is only executed if the value evaluates to true'
  unless:
    $ref: 'http://waml.automate.website/draft-0.2/expression-schema#'
    description: 'If set, the step is only executed if the value evaluates to false'

```
## Enter key sequence
```
id: 'http://waml.automate.website/draft-0.2/enter-command-schema#'
$schema: 'http://json-schema.org/draft-04/schema#'
title: Enter key sequence
description: Send a sequence of key strokes to an element.
properties:
  setValue:
    description: Send a sequence of key strokes to an element.
    $ref: 'http://waml.automate.website/draft-0.2/enter-criteria-schema#'
additionalProperties: false

```
## Click on the given element
```
id: 'http://waml.automate.website/draft-0.2/click-command-schema#'
$schema: 'http://json-schema.org/draft-04/schema#'
title: Click on the given element
description: Clicks on the given visible element.
properties:
  click:
    description: A CSS selector as value or a hash of conditionals.
    oneOf:
      - $ref: 'http://waml.automate.website/draft-0.2/expression-schema#'
      - $ref: 'http://waml.automate.website/draft-0.2/click-criteria-schema#'
additionalProperties: false

```
## Text enter criteria
```
id: 'http://waml.automate.website/draft-0.2/enter-criteria-schema#'
$schema: 'http://json-schema.org/draft-04/schema#'
title: Text enter criteria
description: Qualifier for element which gets the new text.
properties:
  selector:
    $ref: 'http://waml.automate.website/draft-0.2/expression-schema#'
    description: CSS selector of element to select.
  text:
    $ref: 'http://waml.automate.website/draft-0.2/expression-schema#'
    description: Text to set.
additionalProperties: false
required:
  - selector
  - text

```
## Option criteria
```
id: 'http://waml.automate.website/draft-0.2/option-criteria-schema#'
$schema: 'http://json-schema.org/draft-04/schema#'
title: Option criteria
description: Qualifier for select an option from a select.
properties:
  index:
    oneOf:
      - $ref: 'http://waml.automate.website/draft-0.2/expression-schema#'
      - type: number
    description: Option index (selectByIndex)
  name:
    $ref: 'http://waml.automate.website/draft-0.2/expression-schema#'
    description: Name of option element to get selected (selectByName)
  value:
    $ref: 'http://waml.automate.website/draft-0.2/expression-schema#'
    description: Value of option element to get selected (selectByValue)
  text:
    $ref: 'http://waml.automate.website/draft-0.2/expression-schema#'
    description: Text of option element to get selected (selectByText)
additionalProperties: false
minProperties: 1

```
## Parent conditionals
```
id: 'http://waml.automate.website/draft-0.2/parent-criteria-schema#'
$schema: 'http://json-schema.org/draft-04/schema#'
title: Parent conditionals
description: Qualifier for parent element selection.
properties:
  selector:
    $ref: 'http://waml.automate.website/draft-0.2/expression-schema#'
    description: CSS selector of element to select.
  text:
    $ref: 'http://waml.automate.website/draft-0.2/expression-schema#'
    description: Select element which contains the given text.
additionalProperties: false

```
## Option criteria
```
id: 'http://waml.automate.website/draft-0.2/select-criteria-schema#'
$schema: 'http://json-schema.org/draft-04/schema#'
title: Option criteria
description: Qualifier for select an option from a select.
properties:
  selector:
    $ref: 'http://waml.automate.website/draft-0.2/expression-schema#'
    description: CSS selector of element to select.
  option:
    description: Criteria of option to select.
    $ref: 'http://waml.automate.website/draft-0.2/option-criteria-schema#'
additionalProperties: false
required:
  - option

```
## Click conditionals
```
id: 'http://waml.automate.website/draft-0.2/click-criteria-schema#'
$schema: 'http://json-schema.org/draft-04/schema#'
title: Click conditionals
description: Qualifier for click command.
properties:
  selector:
    $ref: 'http://waml.automate.website/draft-0.2/expression-schema#'
    description: CSS selector of element to select.
  text:
    $ref: 'http://waml.automate.website/draft-0.2/expression-schema#'
    description: Select element which contains the given text.
  timeout:
    description: 'Maximal time [ms] to wait for the element which meets the given criteria.'
    oneOf:
      - type: number
      - $ref: 'http://waml.automate.website/draft-0.2/expression-schema#'
  parent:
    description: Presence of the parent element according given creteria.
    oneOf:
      - $ref: 'http://waml.automate.website/draft-0.2/expression-schema#'
      - $ref: 'http://waml.automate.website/draft-0.2/parent-criteria-schema'
additionalProperties: false

```
## Ensure conditionals
```
id: 'http://waml.automate.website/draft-0.2/ensure-criteria-schema#'
$schema: 'http://json-schema.org/draft-04/schema#'
title: Ensure conditionals
description: Conditionals to precise the criteria of ensure command.
properties:
  selector:
    $ref: 'http://waml.automate.website/draft-0.2/expression-schema#'
    description: CSS selector of element to select.
  visible:
    description: Select visible or invisible elements only.
    oneOf:
      - $ref: 'http://waml.automate.website/draft-0.2/expression-schema#'
      - type: boolean
  text:
    $ref: 'http://waml.automate.website/draft-0.2/expression-schema#'
    description: Select element which contains the given text.
  timeout:
    description: 'Maximal time [ms] to wait for the element which meets the given criteria.'
    oneOf:
      - $ref: 'http://waml.automate.website/draft-0.2/expression-schema#'
      - type: number
additionalProperties: false

```
## Expression
```
id: 'http://waml.automate.website/draft-0.2/expression-schema#'
$schema: 'http://json-schema.org/draft-04/schema#'
title: Expression
description: An expression is a evaluable statement that can be utilized on certain properties.
type:
  - string
  - boolean

```