StyleFrame
==========

A library that wraps pandas and openpyxl and allows easy styling of dataframes in excel.

Installation:
-------------
::

    $ pip install styleframe


Testing:
--------

You can make sure everything works as expected by running StyleFrame's unittests:
::

    from StyleFrame import tests

    tests.run()


Some usage examples
-------------------

StyleFrame constructor supports all the ways you are used to initiate pandas dataframe.
An existing dataframe, a dictionary or a list of dictionaries:
::

    from StyleFrame import StyleFrame, Styler, utils

    sf = StyleFrame({'col_a': range(100)})


Applying a style to rows that meet a condition using pandas selecting syntax.
In this example all the cells in the `col_a` column with the value > 50 will have
blue background and a bold, sized 10 font:
::


    sf.apply_style_by_indexes(indexes_to_style=sf[sf['col_a'] > 50],
                              cols_to_style=['col_a'],
                              styler_obj=Styler(bg_color=utils.colors.blue, bold=True, font_size=10))

Creating ExcelWriter used to save the excel:
::

    ew = StyleFrame.ExcelWriter(r'C:\my_excel.xlsx')
    sf.to_excel(ew)
    ew.save()

It is also possible to style a whole column or columns, and decide whether to style the headers or not:
::

    sf.apply_column_style(cols_to_style=['a'], styler_obj=Styler(bg_color=utils.colors.green),
                          style_header=True)


API documentation
-----------------
Given that `sf = StyleFrame(...)` :

Styling by indexes
^^^^^^^^^^^^^^^^^^
::

    sf.apply_style_by_indexes(indexes_to_style=None, cols_to_style=None,
                              styler_obj=Styler(bg_color=utils.colors.white,
                              bold=False, font_size=12, font_color=utils.colors.black,
                              number_format=number_formats.general),
                              protection=False)

Applies a certain style to the provided indexes in the dataframe to the provided columns.
Parameters:
::

    indexes_to_style: indexes to apply the style to
    cols_to_style: the columns to apply the style to, if not provided all the columns will be styled
    styler_obj: a StyleFrame.Styler object
    protection: to protect the cell from changes or not
   

Styling by columns
^^^^^^^^^^^^^^^^^^
::

    sf.apply_column_style(cols_to_style=None,
                          styler_obj=Styler(bg_color=utils.colors.white, bold=False, font_size=12,
                          font_color=utils.colors.black, style_header=False,
                          number_format=number_formats.general),
                          protection=False)

Apply a style to a whole column.
Parameters:
::

    cols_to_style: the columns to apply the style to
    styler_obj: a StyleFrame.Styler object
    protection: to protect the column from changes or not

Styling headers only
^^^^^^^^^^^^^^^^^^^^
::

    sf.apply_headers_style(styler_obj=Styler(bg_color=colors.white, bold=True, font_size=12, font_color=colors.black,
                           number_format=number_formats.general), 
                           protection=False)


Apply style to the headers only.
Parameters:
::

        styler_obj: a StyleFrame.Styler object
        protection: to protect the column from changes or not


Renaming columns
^^^^^^^^^^^^^^^^
::

        sf.rename(columns=None, inplace=False)

Rename the underlying dataframe's columns.
Parameters:
::

        columns: a dictionary, old_col_name -> new_col_name
        inplace: whether to rename the columns inplace or return a new StyleFrame object
        return: None if inplace=True, StyleFrame if inplace=False


Setting columns width
^^^^^^^^^^^^^^^^^^^^^
::

    sf.set_column_width(columns, width)

Set the width of the given columns
Parameters:
::

        columns: a single or a list/tuple of column name, index or letter to change their width
        width: numeric positive value of the new width

::

    set_column_width_dict(self, col_width_dict)

Parameters:
::

        col_width_dict: a dictionary from tuples of columns to the desired width


Setting rows height
^^^^^^^^^^^^^^^^^^^
::

    sf.set_row_height(rows, height)


Set the height of the given rows.
Parameters:
::

        rows: a single row index, list of indexes or tuple of indexes to change their height
        height: numeric positive value of the new height

::

    sf.set_column_width_dict(self, col_width_dict)

Parameters:
::

    sf.set_row_height_dict: a dictionary from tuples of rows to the desired height


