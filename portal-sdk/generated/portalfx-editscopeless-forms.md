
<a name="editscopeless-forms"></a>
## EditScopeless Forms

<a name="editscopeless-forms-difference-between-editscope-backed-forms-and-editscope-less-forms"></a>
### Difference between editscope backed forms and editscope-less forms

<a name="editscopeless-forms-initial-value-and-dirty-state"></a>
### Initial Value and Dirty State

New Controls APIs support creating forms without initializing their editscope. This makes the initialization of the Controls light-weight (i.e. extension developers do need to worry about coupling the right editscope accessor).
Since the editscope is not tied to each control anymore, there is no state associated with the controls. 

From the extension developer's point of view this means two things:

1. There is no concept of initial value for these controls. If you want to initialize the value of a control then you just need to set the value.

```ts
textboxViewModel.value("Some Initial Value");
```  

2. Extension developers have the freedom to control dirty state of control. 

```ts
textboxViewModel.dirty(true);
```  
 

<a name="editscopeless-forms-controls-namespace"></a>
### Controls Namespace

All the new controls are located in the "Fx/Controls" namespace.

```ts
import * as Section from "Fx/Controls/Section";
import * as TextBox from "Fx/Controls/TextBox";
``` 

List of all the new controls that are available in "Fx/Controls":

1. Button
1. CheckBox
1. CustomHtml
1. DatePicker
1. DateTimePicker
1. DateTimeRangePicker
1. DayPicker
1. DropDown
1. DurationPicker
1. FileUpload
1. MultiLineTextBox
1. NumericTextBox
1. OptionsGroup
1. PasswordBox
1. RadioButton
1. RangeSlider
1. Section
1. Slider
1. TabControl
1. TextBox
1. TimePicker
1. TriStateCheckBox

<a name="editscopeless-forms-initializing-controls"></a>
### Initializing Controls

The controls are initialized through a factory method called `create()`. This function returns an interface. 

For example,

invoking the `create()` method to create a TextBox with specific label, subLabel and a collection of validations.

```ts
import * as TextBox from "Fx/Controls/TextBox";

const firstNameViewModel = TextBox.create(container, {
            label: "First Name",
            subLabel: "Try: John",
            validations: [
                new Validations.Required(ClientResources.emptyFirstName),
                new Validations.RegExMatch("^[a-zA-Z]+", `${ClientResources.startsWithLetterValidationMessage} <a href="https://www.bing.com/search?q=Personal+names+around+the+world" target="_blank">${ClientResources.clickForMoreInfo}</a>`)
            ]
        });
```

<a name="editscopeless-forms-using-the-loading-indicator-for-dropdown"></a>
### Using the loading indicator for dropdown

Ibiza SDK now supports showing loading indicator when the data is asynchronously loaded by an AJAX call that takes time to populate the dropdown.

Here is an example of a dropdown that implements a loading indicator

```ts

// Controls Namespace
import * as DropDown from "Fx/Controls/DropDown";

// Initialize control with no data. Set loading indicator to true
const dropDownViewModel = DropDown.create<string>(container, {
            label: ClientResources.spouse,
            validations: [ new Validations.Required(ClientResources.emptySpouse) ],
            loading: true  // ...and dynamically switch to 'false' once the dropdown items are loaded.
        });

// fetch data asynchronously and remove loading indicator on data load
const dropdownDataPromise = Q(model.people.fetch("", container)).then((people) => {
            const dropDownItems = people.data.mapInto(container, (childLifetime: MsPortalFx.Base.LifetimeManager, person: SamplesExtension.DataModels.Person) => {
                return {
                    text: person.name(),
                    value: person.name()
                };
            }, dropDownViewModel.items);
            dropDownViewModel.loading(false);
        });
```

<a name="editscopeless-forms-customizing-alert-on-form-close"></a>
### Customizing Alert on Form Close

SDK Provides two ways to configure the behavior of Alert i.e. the pop-up that shows up when user tries to close a form with unsaved edits. 

For example, 

In this scenario we have suppressed the alert by setting the value to `FxViewModels.AlertLevel.None`

```ts
form.configureAlertOnClose(FxViewModels.AlertLevel.None);
```

The other overload of this function can be used for more complex scenarios say when an extension developer chooses to compute the value of Alert's behavior and message function overload.

For example, in this scenario extension developer is dynamically setting the behavior of alert and message based on the checkbox and textBox.

```ts

this._container.form.configureAlertOnClose(ko.computed(container, () => {
                        return {
                            showAlert: configureCheckBox.value(),
                            message: configureMessageTextBox.value()
                        }
                    }));

```

<a name="editscopeless-forms-customizing-alert-on-form-close-other-css-classes-that-can-be-useful"></a>
#### Other CSS classes that can be useful

1. msportalfx-docking-header
1. msportalfx-docking-body
1. msportalfx-docking-footer
1. msportalfx-padding

As the name suggests msportalfx-docking-* classes are helpful when you need to dock elements at the header, body or footer of the blade. 
msportalfx-padding class is useful to add 10 x 10 padding to the blade.

Managing the styling of blade through these css classes gives extension developers flexibility to use Blades as a canvas.
Unlike previous version of SDK, No-PDL blades do not add any padding / docking content behavior by default. Thus making it easy for extension developers to manage the styling.

<a name="editscopeless-forms-replacing-action-bar-with-button"></a>
### Replacing Action Bar with Button

<a name="editscopeless-forms-replacing-action-bar-with-button-implement-custom-styling"></a>
#### Implement custom styling

Extension developers can use out-of-the-box CSS classes to dock a button at the bottom of blade and make it look like Action Bar.

This sample shows how to replace the action bar by docking a button and errorInfo box at the bottom of blade using `msportalfx-docking-footer` css class.
`msportalfx-padding` is used to add 10 x 10 padding to the docked footer

```html

<div class='msportalfx-docking-footer msportalfx-padding'>
    <div data-bind='pcControl: errorBox, visible: showErrorBox'></div>
    <div data-bind='pcControl: okButton' class='ext-ok-button'></div><a>Link</a>
</div>

```

<a name="editscopeless-forms-replacing-action-bar-with-button-implementing-blade-close-behavior"></a>
#### Implementing blade close behavior

```ts

const okButtonClick = () => {
    container.closeCurrentBlade({
                            firstName: firstNameViewModel.value(),
                            lastName: lastNameViewModel.value(),
                            spouse: dropDownViewModel.value(),
                            password: passwordViewModel.value(),
                        });
};
```