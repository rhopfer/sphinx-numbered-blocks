This is a extension for [Sphinx](http://www.sphinx-doc.org/) to create custom numbered environments like definitions, examples or exercises in html documents.
It was originally written for the online book ["Introduction to Digital Circuits"](https://bibl.ica.jku.at/).


# Installation

Make following changes in `conf.py`:

* Add the path to `numbered_blocks.py` to system path, e.g.
```python
  sys.path.insert(0, os.path.abspath('../ext'))
```

* Add extension, e.g.
```python
  extensions = ['sphinx.ext.mathjax', 'numbered_blocks']
```

# Configuration

First define a new block definition inside the *numbered_blocks* configuration option, e.g.
```python
numbered_blocks = [{ 'name': 'definition' }]
```

A definition knows following options:

`name` (String)  
  Name of the block directive

`reference` (String)  
    Name of the reference role. Set to False to disable references for this Block.  
	Default: name + '-ref'

`label-format` (Format string)  
    Format of label  
	Default: name.capitalize() + ' %s'

`reference-format` (Format string)  
    Format of references  
	Default: label-format

`title-format` (Format string)  
    Format of title  
	Default: '%s'

`title-separator` (String)  
    Separator between label and title  
	Default: ': '

`numbered` (Boolean)
    Number blocks  
	Default: True  

`wrap-content` (Format string)  
    Wrap content  
	Default: '%'

`counter` (String)
    Explicite internal counter. Set this if you want to share a counter between two different block types.  
	Default: name

`title-position` ('top' or 'bottom')  
	Position of the title. Not available for tables and figures. For tables use the CSS attribute *caption-side* instead.  
	Default: 'top'

# Use

## Directive

```rest
.. definition:: The Title
   :name: Definition Name

   The Content
```

Options:

`:name:` String  
    Name to reference

`:class:` String  
    Additional optional classes

`:id:` String  
    Set explicite ID

`:nonumber:` Empty  
    Disable numbering


Result:
```html
<div id="definition-0" class="numbered-block definition">
  <span class="title">
  <span class="label">Definition 1.1</span>
  <span class="separator">: </span>
  The Title
  </span>
  <p>The Content</p>
</div>
```

## References

``:defnition-ref:`Definition Name```  
=> Definition 1.1

``:defnition-ref:`Explicite Title <Definition Name>```  
=> Explicite Title

``:defnition-ref:`Definition Name + (Suffix)```  
=> Definition 1.1 (Suffix)


## Numbered figures and tables

There are special handles for figures and tables. Just add a definition in the common way:
```python
numbered_blocks = [ ..., {'name', 'figure'}]
```

## Known Issues

Normal references ``:ref:`table name` `` for tables create wrong labels.
Normal references ``:ref:`figure name` `` for figures silently ignored.
