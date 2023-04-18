Jump to @ sign, this is your vim-refactoring starting point.

## Example 1

@
Rename "width" to "length"

```
  METHOD get_text.
    result = |Invalid width.|.
  ENDMETHOD.
```

5j      "5 lines down"
fw      "forward to first occurrence of w"
cw      "change word"
length  "enter text"

## Example 2

@
Correct typing error "ont" to "not"

```
  METHOD get_text.
    result = |File could ont be read.|.
  ENDMETHOD.
```

/ont<cr>  "search for 'ont'"
n         "next occurrence"
x         "delete character"
p         "paste content of default register (o) after cursor"

## Example 3

@
Remove prefixes of parameters

```
  METHODS:
    process
      IMPORTING
        i_text_before       TYPE string
        i_width             TYPE i
      RETURNING
        VALUE(r_text_after) TYPE stringtab.
```

/i_<cr>   "search for 'i_'; this will jump to the beginning of i_text_before"
ctrl+2, r "rename in file; this will rename all occurrences of i_text_before"
2x        "remove character under cursor and next one"
<cr>      "end renaming"
n         "find next occurrence of last searched string ('i_'); this will jump to the beginning of i_width"
ctrl+2, r "rename in file; this will rename all occurrences of i_width"
2x        "remove character under cursor and next one"
<cr>      "end renaming"
2j        "2 lines down"
fr        "forward to first occurrence of r"
ctrl+2, r "rename in file; this will rename all occurrences of r_text_after"
2x        "remove character under cursor and next one"
<cr>      "end renaming"

## Example 4

@
Remove prefix 'lv_' from multiple variables in local scope


```
  METHOD multiplication.
    DATA(lv_left) = iv_left.
    DATA(lv_right) = iv_right.
    add_line(
      EXPORTING
        iv_left   = lv_left
        iv_right  = lv_right
    ).
    WHILE lv_left > 1.
      calculate_next_line(
        CHANGING
          cv_left  = lv_left
          cv_right = lv_right
      ).
      add_line(
        EXPORTING
          iv_left   = lv_left
          iv_right  = lv_right
      ).
    ENDWHILE.
    rv_result = calculate_result( ).
    IF iv_write_calculation = abap_true.
      write_calculation( iv_result = rv_result ).
    ENDIF.
  ENDMETHOD.
```

:       "Enter command mode"
%       "For the whole file"
s       "Substitute"
/lv_    "Find lv_"
//      "Substitute with nothing
g       "Substitute all occurrences"

<cr>    "Run command"

## Example 5

@
