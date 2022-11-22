# Basic use cases

The validity component covers any kind of form element, here we listed all the possible validation can be handled with the constraint validation from browser. There are 3 kinds:


[Numeric value](#numericvalue):
- [Number](#number)
- [Range](#range)
- [Date](#datetypedatemonthweektimedatetimelocal)
- [Month](#month)
- [Week](#week)
- [time](#time)
- [Datetime](#datetimelocal)

[String value](#stringvalue)
- [text](#texttextpasswordemailurl)
- [password](#password)
- [url](#url)
- [email](#email)

[Textarea](#textarea)

Keep in mind in this page, we tried to list down most common input types that may involve validation. And provide examples of implementation with only browser API, there is another topic for the [usage of custom validation function](/01%20-%20API/#validatorcallbackcallback) and how to [customize the default error message](/03%20-%20Advanced%20usage/02%20-%20Customize%20error/) from browser API.

## Numeric value

list of attributes available for validation:
- step
- max
- min

## Number

Number is the most basic numeric input type, most of the modern browsers already blocked the input from none numeric characters.
```hbs
<ValidatorContainer as |v|>
  <v.validity @model={{hash number=this.number}} as |validity|>
    <input
      type="number"
      value={{this.number}}
      onInput={{this.onInput}}
      required
      step="0.5"
      min="30.00"
      max="75.00"
      name="number"
    />
    {{#if validity.errorMessage.number}}
      <br />
      <br />
      {{validity.errorMessage.number}}
    {{/if}}
  </v.validity>
</ValidatorContainer>
```

## Range

Range is very similar to `number`, but with different visual. Thanks for the restriction of input method, the user cannot enter any value manually which leads to invalid.
```hbs
<ValidatorContainer as |v|>
  <v.validity @model={{hash range=this.range}} as |validity|>
    <input
      type="range"
      value={{this.range}}
      onInput={{this.onInput}}
      required
      step="0.5"
      min="30.00"
      max="75.00"
      name="range"
    />
    <div>value: {{this.range}}</div>
    {{#if validity.errorMessage.range}}
      <br />
      <br />
      {{validity.errorMessage.range}}
    {{/if}}
  </v.validity>
</ValidatorContainer>

```

## date (type=date|month|week|time|datetime-local)

Most of the modern browsers can render a calender for date input and already black out the unavailable dates for selection. However the error can still arise with typing.
```hbs
<ValidatorContainer as |v|>
  <v.validity @model={{hash date=this.date}} as |validity|>
    <input
      type="date"
      value={{this.date}}
      onInput={{this.onInput}}
      required
      step="7"
      min="2021-01-15"
      max="2021-09-15"
      name="date"
    />
    {{#if validity.errorMessage.date}}
      <br />
      <br />
      {{validity.errorMessage.date}}
    {{/if}}
  </v.validity>
</ValidatorContainer>
```

### month
```hbs
<ValidatorContainer as |v|>
  <v.validity @model={{hash month=this.month}} as |validity|>
    <input
      type="month"
      value={{this.month}}
      onInput={{this.onInput}}
      required
      step="2"
      min="2021-01"
      max="2021-09"
      name="month"
    />
    {{#if validity.errorMessage.month}}
      <br />
      <br />
      {{validity.errorMessage.month}}
    {{/if}}
  </v.validity>
</ValidatorContainer>
```

### week
```hbs
<ValidatorContainer as |v|>
  <v.validity @model={{hash week=this.week}} as |validity|>
    <input
      type="week"
      value={{this.week}}
      onInput={{this.onInput}}
      required
      step="2"
      min="2021-W30"
      max="2021-W35"
      name="week"
    />
    {{#if validity.errorMessage.week}}
      <br />
      <br />
      {{validity.errorMessage.week}}
    {{/if}}
  </v.validity>
</ValidatorContainer>
```

### time
```hbs
<ValidatorContainer as |v|>
  <v.validity @model={{hash time=this.time}} as |validity|>
    <input
      type="time"
      value={{this.time}}
      onInput={{this.onInput}}
      required
      step="900"
      min="09:30:00"
      max="12:00:00"
      name="time"
    />
    {{#if validity.errorMessage.time}}
      <br />
      <br />
      {{validity.errorMessage.time}}
    {{/if}}
  </v.validity>
</ValidatorContainer>
```

### datetime-local
```hbs
<ValidatorContainer as |v|>
  <v.validity @model={{hash datetime=this.datetime}} as |validity|>
    <input
      type="datetime-local"
      value={{this.datetime}}
      onInput={{this.onInput}}
      required
      step="900"
      min="2021-09-01T09:30:00"
      max="2021-09-30T18:00:00"
      name="datetime"
    />
    {{#if validity.errorMessage.datetime}}
      <br />
      <br />
      {{validity.errorMessage.datetime}}
    {{/if}}
  </v.validity>
</ValidatorContainer>
```


## String value

list of attributes available for validation:
- [pattern](https://developer.mozilla.org/en-US/docs/Web/HTML/Attributes/pattern)
- maxlength
- minlength

### text (text|password|email|url)
```hbs
<ValidatorContainer as |v|>
  <v.validity @model={{hash text=this.text}} as |validity|>
    <input
      type="text"
      value={{this.text}}
      onInput={{this.onInput}}
      name="text"
      pattern="[0-9]{1,3}.[0-9]{1,3}.[0-9]{1,3}.[0-9]{1-3}"
      minlength="10"
      maxlength="13"
      required
    />
    {{#if validity.errorMessage.text}}
      <br />
      <br />
      {{validity.errorMessage.text}}
    {{/if}}
  </v.validity>
</ValidatorContainer>
```

### password
```hbs
<ValidatorContainer as |v|>
  <v.validity @model={{hash password=this.password}} as |validity|>
    <input
      type="password"
      value={{this.password}}
      onInput={{this.onInput}}
      name="password"
      pattern="[0-9a-zA-Z!@#]{8,15}"
      minlength="8"
      maxlength="15"
      required
    />
    {{#if validity.errorMessage.password}}
      <br />
      <br />
      {{validity.errorMessage.password}}
    {{/if}}
  </v.validity>
</ValidatorContainer>
```

### url
```hbs
<ValidatorContainer as |v|>
  <v.validity @model={{hash url=this.url}} as |validity|>
    <input
      type="url"
      value={{this.url}}
      onInput={{this.onInput}}
      name="url"
      pattern="http:.*"
      minlength="10"
      maxlength="15"
      required
    />
    {{#if validity.errorMessage.url}}
      <br />
      <br />
      {{validity.errorMessage.url}}
    {{/if}}
  </v.validity>
</ValidatorContainer>
```

### email
```hbs
<ValidatorContainer as |v|>
  <v.validity @model={{hash email=this.email}} as |validity|>
    <input
      type="email"
      value={{this.email}}
      onInput={{this.onInput}}
      name="email"
      pattern="[a-z0-9]{1,10}@gmail.com"
      minlength="12"
      maxlength="20"
      required
    />
    {{#if validity.errorMessage.email}}
      <br />
      <br />
      {{validity.errorMessage.email}}
    {{/if}}
  </v.validity>
</ValidatorContainer>
```
## Textarea

list of attributes available for validation:
- required
- maxlength
- minlength

```hbs
<ValidatorContainer as |v|>
  <v.validity @model={{hash feedback=this.feedback}} as |validity|>
    <textarea
      name="feedback"
      rows="5"
      cols="30"
      minlength="10" 
      maxlength="40"
      value={{this.feedback}}
      required
      {{on "input" this.onInput}}
      data-test-textarea
    >
      Write something here…
    </textarea>
    {{#if validity.errorMessage.feedback}}
      <br />
      <br />
      {{validity.errorMessage.feedback}}
    {{/if}}
  </v.validity>
</ValidatorContainer>
```
