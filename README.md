## Call ProcessWire API Functions Inside STRING

Current status : **BETA**

### Each called method must return string value !

I added all functions, but not tested all. I focused page(), page()->render and field properties (label, description and notes). I also tested some basic pages() api calls.

Your API calls must start with `{` and must end with `}`. For use multiple arguments inside functions, separate arguments with `~` char.

**NOTE** If you pass directly arguments to api `{page(title)}`, this call will check for `requestedApiCall()->get(arguments)`.

## USAGE

```php
processString(string, page, language);
```

- Get page title
```php
<?php
$str = "You are here : {page:title}";
echo processString($str);
?>
```

- Get page children render result
```php
<?php
$str = "Lorem ipsum dolor sit amet, consectetur adipisicing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat.<hr>{page:render:children}";
echo processString($str);
?>
```

- Get homepage title
```php
<?php
$str = "You can visit our <a hre='{pages(1):url}'>{pages:get(1):title}</a>";
echo processString($str);
?>
```

- Get title field label, description or notes
```php
<?php
$str = "Our title field properties are : label: {label(title)} - description: {description(title)} - notes: {notes(title)}";
echo processString($str);
?>
```

- Multiple examples
```php
<?php
$str = "
    <ul class='uk-list uk-list-striped'>
        <li><b>01: GET FIELD LABEL</b> <code>&#123;label(title)&#125;</code> <b>RESULT :</b> <code>{label(title)}</code></li>
        <li><b>02: GET FIELD LABEL WITH PREFIX</b> <code>&#123;label(title~=> )&#125;</code> <b>RESULT :</b> <code>{label(title~=> )}</code></li>
        <li><b>03: GET FIELD LABEL WITH SUFFIX</b> <code>&#123;label(title~~ <=)&#125;</code> <b>RESULT :</b> <code>{label(title~~ <=)}</code></li>
        
        <li><b>04: GET FIELD DESCRIPTION</b> <code>&#123;description(title)&#125;</code> <b>RESULT :</b> <code>{description(title)}</code><br>
        <li><b>05: GET FIELD DESCRIPTION WITH PREFIX</b> <code>&#123;description(title~=> )&#125;</code> <b>RESULT :</b> <code>{description(title~=> )}</code></li>
        <li><b>06: GET FIELD DESCRIPTION WITH SUFFIX</b> <code>&#123;description(title~~ <=)&#125;</code> <b>RESULT :</b> <code>{description(title~~ <=)}</code></li>
        
        <li><b>07: GET FIELD NOTES</b> <code>&#123;notes(title)&#125;</code> <b>RESULT :</b> <code>{notes(title)}</code><br>
        <li><b>08: GET FIELD NOTES WITH PREFIX</b> <code>&#123;notes(title~=> )&#125;</code> <b>RESULT :</b> <code>{notes(title~=> )}</code></li>
        <li><b>09: GET FIELD NOTES WITH SUFFIX</b> <code>&#123;notes(title~~ <=)&#125;</code> <b>RESULT :</b> <code>{notes(title~~ <=)}</code></li>
        
        <li><b>10: GET PAGE TITLE</b> <code>&#123;page(title)&#125;</code> <b>RESULT :</b> <code>{page(title)}</code></li>
        <li><b>11: GET PAGE TITLE</b> <code>&#123;page:title&#125;</code> <b>RESULT :</b> <code>{page:title}</code></li>
        <li><b>12: GET PAGE RENDER TITLE</b> <code>&#123;page:render:title&#125;</code> <b>RESULT :</b> <code>{page:render:title}</code></li>
        
        <li><b>12: GET HOMEPAGE TITLE</b> <code>&#123;pages:get(template=home):title&#125;</code> <b>RESULT :</b> <code>{pages:get(template=home):title}</code></li>
        <li><b>13: GET HOMEPAGE TEMPLATE ID</b> <code>&#123;pages:get(template=home):template:id&#125;</code> <b>RESULT :</b> <code>{pages:get(template=home):template:id}</code></li>
    </ul>
    ";
echo processString($str);
?>
```