---
title:  "Form-specific Element Templates in Drupal 8"
date:   2017-03-19 15:04:23
categories: Engineering
published: true
tags: Drupal PHP
---
Out of the box, Drupal 8 uses a common template for all form elements called
`form-element.html.twig`. Today we'll explore how to override what Drupal gives
us by using form-specific and element-specific template suggestions, such as `form-element--user-login--username.html.twig`, where `user-login` is our form ID and `username` is our form element name. As another example, we could override the template for the search box within a specific search form that doesn't affect any other form element on the site, _even if they share the same element name_.

On the surface, this seems like it'd be a simple template suggestion. However, this was a little more complicated than meets the eye because when you're working with a form element in the preprocess layer (or within a suggestion hook), Drupal does not give you any context outside of the element. This means that an element doesn't know anything about the form that's rendering it, but it is this context we need to be able to set a form-specific template suggestion.

First we do a `hook_form_alter` to add in a `#form_id` attribute to all children of the form:

``` php
<?php
function _MYMODULE_form_alter_elements(&$element, $form_id) {
  $children = Element::children($element);
  foreach ($children as $child_key) {
    $element[$child_key]['#form_id'] = $form_id;
    _kraken_form_alter_elements($element[$child_key], $form_id);
  }
}
function MYMODULE_form_alter(&$form, &$form_state, $form_id) {
  _MYMODULE_form_alter_elements($form, $form_id);
  // ...
}
```

Once we have the form ID available then it's just a simple suggestions alter:

``` php
<?php
function MYMODULE_theme_suggestions_form_element_alter(array &$suggestions, array $variables) {
  $elementId = str_replace('-', '_', $variables['element']['#id']);
  $formId = str_replace('-', '_', $variables['element']['#form_id']);
  $suggestions[] = 'form_element__' . $formId . '__' . $elementId;
}
```


If you're looking for some other template suggestions for form elements such as
`form-element--[form-id]--[element-type].html.twig` or `form-element--type--[element-type].html.twig`, you can use the mechanism shown above, or you could try out the [Themable forms](https://www.drupal.org/project/themable_forms) module. As of this writing it's in Alpha status, but the [code](http://cgit.drupalcode.org/themable_forms/tree/themable_forms.module) is dead-simple; I consider it reasonable for production use.


