Python Code of Markdown File Example
====================================

.. code:: python



    from mdutils.mdutils import MdUtils
    from mdutils import Html

    mdFile = MdUtils(file_name='Example_Markdown', title='Markdown File Example')

    mdFile.new_header(level=1, title='Overview')  # style is set 'atx' format by default.

    
