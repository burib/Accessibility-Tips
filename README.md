# Accessibility-Tips

Credits goes to: <a href="https://github.com/rumoroso" target="_blank">@rumoroso</a>

Two basic tips about A11y: focus and wai-aria

Focusable elements

One  important tip to follow is to take care about the way in which the user can interact with the widgets. Whole application should allow be used with keyboard… only with keyboard. This means that all interaction elements should be focusable.

To achieve this, the first step is to use interaction elements (buttons, links…) and prevent to apply interaction behaviour to elements that are not (e.g.: try to avoid to use click events in elements like span or div). If it is not possible, the way to transform not interaction elements in interaction elements is using the tabindex attribute. This attribute can have values from -1 to infinite… but the value to use should be “0”… The reason to use this value is because allows the focus in the element, but keep the natural tab order in the document. If you want to know what happens with other values, ask me? ;)

Of course, the focus status should be identified by the user… e.g.: set a border/outline/background-color/… to the pseudo-class :focus in css.

Allowing to be focusable is not enough to guaranty that the behaviour can be fired with the keyboard. I am talking about the event that is applied to the element. If the element is not an interaction element, the click event will not fire keyboard events, so it will be needed to include keyboard events (keypress, keydown, keyup….) and check the keycode to allow or not the functionality (e.g.: we don’t want to collapse/show content if we press the keycode 65 -> key “a”… or yes?).

Finally, it is needed to take care about the elements that get the focus and, because other behaviour, disappear. If the element that has the focus disappears, the focus will be reset to the first focusable element in the document. We could need to set programmatically the focus in that kind of cases.

WAI-Aria

The next list of Aria attributes contains the attributes that we could need in the framework for the 90-95% behaviours that the widgets have. Some of the attributes should be applied because the default html behaviour of the elements doesn’t include the behaviour that we are adding (e.g. the pressed status). In all cases, they are the way in which the A11y API can identify the behaviour/functionality/way to interact/etc. with the widgets and components that we have.

There is a ngAria module in Angular, so we could start to use it (https://code.angularjs.org/1.3.15/docs/api/ngAria). This module applies some of the next attributes according to the directives that we use.

Aria attributes for the content that changes in the page (e.g. notification panel):
•	aria-live -> the main meaning is to say “hi, this element has content that can change”, so the screen reader will be alerted when that happens:
o	polite -> the screen reader will read the change after it finished what it is reading (recommended for 99.9% of the cases)
o	assertive -> the screen reader will stop reading to read the change
o	off -> default value and when it is used, the changes are read only when the assistive technology is currently focused in the region/element.
•	aria-atomic -> this attribute say to the A11y API what should be read by the screen reader (or other assistive technology):
o	true -> it will read all the content inside of the element that has “aria-live”
o	false -> it will read only the content that has changed (be careful with the use). It is the default value
•	aria-relevant -> it says to the A11y API what changes should be notified:
o	additions
o	removals
o	text
o	all
o	additions text -> default value

The main attribute to use is “aria-live”, the advice is to add “aria-atomic” at the same time. The last one could be omitted (depending on the context).
____________________________________________________________________________________________________________________

Aria attribute to use in elements that can be hidden:
•	aria-hidden:
o	true
o	false
This attribute could/should be updated with js. For instance, if we have content that is hidden, the element should have aria-hidden=”true”, but when we change the status of that content and is shown, we should change the value of the attribute or remove it (I prefer to remove it). When the element is hidden again, we have to recover it. This is one of the attributes that ngAria applies if the element is using ngShow or ngHide.
____________________________________________________________________________________________________________________

Aria attribute to use in elements that can be disabled:
•	aria-disabled:
o	true
o	false
This attribute could/should be updated with js.
____________________________________________________________________________________________________________________

Aria attribute to alert about the sorting order in items/rows/columns that are sorted programmatically: 
•	aria-sort:
o	ascending
o	descending
o	none -> default value
o	other -> depending on the algorithm used and if other that ascending or descending
My advice is to use it only in the header that is applying the sorting and change its value according to it. If the column is not sorted, I prefer to remove the attribute. This attribute is applied in the sorting behaviour that the framework has in the tables (review the th that applies the sorting and see how it changes) 
____________________________________________________________________________________________________________________

Aria attribute for selectable elements:
•	aria-selected:
o	true
o	false
o	undefined -> default value. It means that the element is not selectable
This attribute is applied to elements/items that can be selectable. My advice is to use in elements in which we are creating that behaviour.
____________________________________________________________________________________________________________________

Aria attribute for pressed status:
•	aria-pressed:
o	true
o	false
o	mixed -> mixed value for a tri-state toggle button
o	undefined -> default value. It means that the element cannot be pressed
This attribute is applied to elements/items that can have that status pressed (I am not talking about elements that can be pressed… of course, the elements that have the status pressed can be pressed, but they are different things). My advice is to use it in elements in which we are creating that behaviour.
____________________________________________________________________________________________________________________





Of course, there are more aria attributes (roles, status, properties,… http://www.w3.org/TR/wai-aria-1.1/img/rdf_model.svg ), advices, techniques, requirements, etc. that are needed to apply, but we could start with these. I think they are easy to apply… and if someone wants to comment about it, we could discuss it.

Some links:
•	http://www.w3.org/WAI/ 
•	http://www.w3.org/TR/WCAG20/ 
•	http://www.w3.org/TR/wai-aria/ 
•	http://www.w3.org/TR/aria-in-html/
•	https://code.angularjs.org/1.3.15/docs/api/ng/directive/ngDisabled

Tools:
•	http://www.w3.org/WAI/ER/tools/ 

Screen readers:
•	NVDA http://www.nvaccess.org/
•	JAWS http://www.freedomscientific.com/Downloads/JAWS
•	VoiceOver http://www.apple.com/es/accessibility/osx/voiceover/
•	Orca https://wiki.gnome.org/action/show/Projects/Orca 
•	Google Talkback https://play.google.com 

I am sure all that I have written could be improved and so on… but I am tired of writing ;)…
