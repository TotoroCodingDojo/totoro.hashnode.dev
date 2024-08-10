---
title: "Leveraging the Jupyter and IPython display protocol"
datePublished: Sat Aug 10 2024 15:18:26 GMT+0000 (Coordinated Universal Time)
cuid: clzoa6azo000509jve878h3cx
slug: leveraging-the-jupyter-and-ipython-display-protocol
tags: python, jupyter-notebook

---

In python for every object you create there is a `__repr__` method in it which is used to display it wherever you print that variable.

```python
class Student:

    def __init__(self, name, class_name) -> None:
        self.name = name
        self.class_name = class_name

    def __repr__(self):
        return f"Hi! I'm {self.name} of {self.class_name}"

if __name__ == "__main__":
    s = Student("totoro", "5")
    print(s) # Output: Hi! I'm totoro of 5
```

Same in true for Ipython also, but in this case we can give other type of representations like HTML, images, latex.

Example:

```python
class MultiMime:
    
    def __repr__(self):
        return "this is the repr"
    
    def _repr_html_(self):
        return "This <b>is</b> html"
    
    def _repr_markdown_(self):
        return "This **is** markdown"

    def _repr_latex_(self):
        return "$ Latex \otimes mimetype $"
```

If you run this in jupyter notebook, you will get the `_repr_html_` display.

There is a priority on which type of mimetype will be used,

```yml
sphinx:
  config:
    nb_mime_priority_overrides: [
      ['html', 'application/vnd.jupyter.widget-view+json', 10],
      ['html', 'application/javascript', 20],
      ['html', 'text/html', 30],
      ['html', 'image/svg+xml', 40],
      ['html', 'image/png', 50],
      ['html', 'image/gif', 60],
      ['html', 'image/jpeg', 70],
      ['html', 'text/markdown', 80],
      ['html', 'text/latex', 90],
      ['html', 'text/plain', 100]
    ]
```

More details can be found [here](https://jupyterbook.org/en/stable/content/code-outputs.html).
