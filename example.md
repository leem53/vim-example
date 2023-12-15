# Info

This File is using <name your IDE> with the VIM Emulator <name the VIM Plugin>.
The Goal is to describe VIM Refactorings, that are useful for Developers.

Try to create Examples that don't have more then 14 VIM Refactoring Moves!
Code Snippet shouldn't be more then 10 Lines of Code.

# Examples

## Example-1

@
Delete the Word 'Damir'.

``` abap
register(|Damir|);
```

| WHAT                | HOW                             |
|---------------------|---------------------------------|
| search for 'D'      | <kbd>/</kbd>`D`<kbd>enter</kbd> |
| search next Finding | <kbd>n</kbd>                    |
| delete Word         | <kbd>d</kbd><kbd>w</kbd>        |

## Example-1

@
Rename 'width' to 'length'

``` abap
  METHOD get_text.
    result = |Invalid width.|.
  ENDMETHOD.
```

| WHAT                             | HOW                      |
|----------------------------------|--------------------------|
| 5 lines down                     | <kbd>5</kbd><kbd>j</kbd> |
| forward to first occurrence of w | <kbd>f</kbd><kbd>w</kbd> |
| change word                      | <kbd>c</kbd><kbd>w</kbd> |
| enter text                       | `length`<kbd>esc</kbd>   |

## Example-2

@
Correct typing error 'ont' to 'not'

``` abap
  METHOD get_text.
    result = |File could ont be read.|.
  ENDMETHOD.
```

| WHAT                                               | HOW                                                              |
|----------------------------------------------------|------------------------------------------------------------------|
| search for 'ont'                                   | <kbd>/</kbd>`ont`<kbd>enter</kbd>                                |
| next occurrence                                    | <kbd>n</kbd>                                                     |
| delete character                                   | <kbd>x</kbd>                                                     |
| paste content of default register (o) after cursor | <kbd>p</kbd>                                                     |

## Example-3

@
Remove prefixes of parameters

``` abap
  METHODS:
    process
      IMPORTING
        i_text_before       TYPE string
        i_width             TYPE i
      RETURNING
        VALUE(r_text_after) TYPE stringtab.
```

| WHAT                                                                                            | HOW                                                  |
|-------------------------------------------------------------------------------------------------|------------------------------------------------------|
| search for 'i_'; this will jump to the beginning of i_text_before                               | <kbd>/</kbd>`i_`<kbd>enter</kbd>                     |
| rename in file; this will rename all occurrences of i_text_before                               | <kbd>ctrl</kbd><kbd>2</kbd><kbd>r</kbd>              |
| remove character under cursor and next one                                                      | <kbd>2</kbd><kbd>x</kbd>                             |
| end renaming                                                                                    | <kbd>enter</kbd>                                     |
| find next occurrence of last searched string ('i_'); this will jump to the beginning of i_width | <kbd>n</kbd>                                         |
| rename in file; this will rename all occurrences of i_width                                     | <kbd>ctrl</kbd><kbd>2</kbd><kbd>r</kbd>              |
| remove character under cursor and next one                                                      | <kbd>2</kbd><kbd>x</kbd>                             |
| end renaming                                                                                    | <kbd>enter</kbd>                                     |
| 2 lines down                                                                                    | <kbd>2</kbd><kbd>j</kbd>                             |
| forward to first occurrence of r                                                                | <kbd>f</kbd><kbd>r</kbd>                             |
| rename in file; this will rename all occurrences of r_text_after                                | <kbd>ctrl</kbd><kbd>2</kbd><kbd>r</kbd>              |
| remove character under cursor and next one                                                      | <kbd>2</kbd><kbd>x</kbd>                             |
| end renaming                                                                                    | <kbd>enter</kbd>                                     |

## Example-4

@
Remove prefix 'lv_' from multiple variables in local scope

``` abap
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

| WHAT                       | HOW                                              |
|----------------------------|--------------------------------------------------|
| Enter command mode         | <kbd>:</kbd>                                     |
| For the whole file         | <kbd>%</kbd>                                     |
| Substitute                 | <kbd>s</kbd>                                     |
| Find lv_                   | <kbd>/</kbd>`lv_`                                |
| Substitute with nothing    | <kbd>/</kbd><kbd>/</kbd>                         |
| Substitute all occurrences | <kbd>g</kbd>                                     |
| Run command                | <kbd>enter</kbd>                                 |

## Example-5

@
Unchain method declarations

``` abap
CLASS ltc_russian_peasant_multipl DEFINITION FINAL FOR TESTING
  DURATION SHORT
  RISK LEVEL HARMLESS.

  PRIVATE SECTION.
    METHODS:
      acceptance_test FOR TESTING RAISING cx_static_check,
      simple_multiplication FOR TESTING RAISING cx_static_check,
      calculate_result FOR TESTING RAISING cx_static_check,
      calculate_next_line FOR TESTING RAISING cx_static_check,
      add_line_left_even FOR TESTING RAISING cx_static_check,
      add_line_left_odd FOR TESTING RAISING cx_static_check,
      calculate_column_width FOR TESTING RAISING cx_static_check.
ENDCLASS.
```

| WHAT                                    | HOW                                  |
|-----------------------------------------|--------------------------------------|
| 9 lines down                            | <kbd>9</kbd><kbd>j</kbd>             |
| Jump to end of line (:)                 | <kbd>$</kbd>                         |
| Delete character                        | <kbd>x</kbd>                         |
| Delete whole word ('METHODS')           | <kbd>d</kbd><kbd>a</kbd><kbd>w</kbd> |
| One line down                           | <kbd>j</kbd>                         |
| Start recording macro 'q'               | <kbd>q</kbd><kbd>q</kbd>             |
| Jump to beginning of line               | <kbd>0</kbd>                         |
| Jump to next word                       | <kbd>w</kbd>                         |
| Move left two times                     | <kbd>h</kbd><kbd>h</kbd>             |
| Paste from register ('METHODS')         | <kbd>p</kbd>                         |
| Jump to end of line                     | <kbd>$</kbd>                         |
| Replace character under cursor with '.' | <kbd>r</kbd>`.`                      |
| One line down                           | <kbd>j</kbd>                         |
| End recording macro                     | <kbd>q</kbd>                         |
| Apply macro 'q' six times               | <kbd>6</kbd><kbd>@</kbd><kbd>q</kbd> |

## Example-6

@
Unchain few method declarations

``` abap
    METHODS:
      text_is_broken_length_9 FOR TESTING RAISING cx_static_check,
      text_is_broken_length_14 FOR TESTING RAISING cx_static_check.
```

| WHAT                                           | HOW                                      |
|------------------------------------------------|------------------------------------------|
| Search ':'                                     | <kbd>/</kbd>`:`<kbd>enter</kbd>          |
| Delete character                               | <kbd>x</kbd>                             |
| Delete whole word ('METHODS')                  | <kbd>d</kbd><kbd>a</kbd><kbd>w</kbd>     |
| One line down                                  | <kbd>j</kbd>                             |
| Jump to next word                              | <kbd>w</kbd>                             |
| Move left two times                            | <kbd>h</kbd><kbd>h</kbd>                 |
| Block selection                                | <kbd>ctrl</kbd><kbd>v</kbd>              |
| One line down                                  | <kbd>j</kbd>                             |
| Paste from register ('METHODS')                | <kbd>p</kbd>                             |
| Jump to last character                         | <kbd>$</kbd>                             |
| Replace character under cursor with '.'        | <kbd>r</kbd>`.`                          |

## Example-7

@
Increase all arguments of the roll-calls by one

``` abap
    DO 1000 TIMES.
      mo_cut->roll( 6 ).
      mo_cut->roll( 9 ).
      mo_cut->roll( 1 ).
      mo_cut->roll( 8 ).
      mo_cut->roll( 2 ).
      mo_cut->roll( 7 ).
      mo_cut->roll( 3 ).
      mo_cut->roll( 6 ).
      mo_cut->roll( 4 ).
      mo_cut->roll( 5 ).
      mo_cut->roll( 5 ).
      mo_cut->roll( 4 ).
      mo_cut->roll( 6 ).
      mo_cut->roll( 3 ).
      mo_cut->roll( 7 ).
      mo_cut->roll( 2 ).
      mo_cut->roll( 8 ).
      mo_cut->roll( 1 ).
      mo_cut->roll( 9 ).
      mo_cut->roll( 0 ).
      CLEAR mo_cut.
      mo_cut = NEW lcl_game( ).
    ENDDO.
```

| WHAT                              | HOW                                  |
|-----------------------------------|--------------------------------------|
| Five lines down                   | <kbd>5</kbd><kbd>j</kbd>             |
| Jump to '6'                       | <kbd>f</kbd>`6`                      |
| Block selection                   | <kbd>ctrl</kbd><kbd>v</kbd>          |
| 19 lines down                     | <kbd>1</kbd><kbd>9</kbd><kbd>j</kbd> |
| Increase number under cursor by 1 | <kbd>ctrl</kbd><kbd>a</kbd>          |

## Example-8

@
Change X to lower case

``` abap
result = VALUE #( ( rolls = 'X X X X X X X X X X X X' result = 300 ) ).
```

| WHAT                                          | HOW                                  |
|-----------------------------------------------|--------------------------------------|
| Four lines down                               | <kbd>4</kbd><kbd>j</kbd>             |
| Jump to 'X'                                   | <kbd>f</kbd>`X`                      |
| Select everything within the current ''-block | <kbd>v</kbd><kbd>i</kbd>`'`          |
| Turn selection to lower case                  | <kbd>u</kbd>                         |

## Example-9

@
Insert line breaks after method name and parameter group

``` abap
METHODS get_element_at_position IMPORTING iv_position      TYPE i
                                RETURNING VALUE(rv_result) TYPE string.
```

| WHAT                                           | HOW                           |
|------------------------------------------------|-------------------------------|
| Four lines down                                | <kbd>4</kbd><kbd>j</kbd>      |
| Jump to space                                  | <kbd>f</kbd><kbd>space</kbd>  |
| Jump two more times                            | <kbd>;</kbd><kbd>;</kbd>      |
| Block selection                                | <kbd>ctrl</kbd><kbd>v</kbd>   |
| One line down                                  | <kbd>j</kbd>                  |
| Replace selection with line break              | <kbd>r</kbd><kbd>enter</kbd>  |
| Jump to previous space                         | <kbd>F</kbd><kbd>space</kbd>  |
| Replace character under cursor with line break | <kbd>r</kbd><kbd>enter</kbd>  |
| Format code                                    | <kbd>shift</kbd><kbd>f1</kbd> |

## Example-10

@
Introduce parameter

``` abap
CLASS lcl_frame DEFINITION.
  PUBLIC SECTION.
    DATA attribute TYPE string.
    
    METHODS constructor.
ENDCLASS.

CLASS lcl_frame IMPLEMENTATION.

  METHOD constructor.
    attribute = parameter.
  ENDMETHOD.

ENDCLASS.
```

| WHAT                  | HOW                                                                |
|-----------------------|--------------------------------------------------------------------|
| Search and jump to''' | <kbd>/</kbd><kbd>'</kbd><kbd>enter<kbd>                            |
| Change rest of line   | <kbd>C</kbd>                                                       |
| Enter text            | `parameter`<kbd>esc</kbd>                                          |
| One line up           | <kbd>k</kbd>                                                       |
| Two times left        | <kbd>h</kbd><kbd>h</kbd>                                           |
| Jump to definition    | <kbd>g</kbd><kbd>d</kbd>                                           |
| One word forward      | <kbd>w</kbd>                                                       |
| Enter insert-mode     | <kbd>i</kbd>                                                       |
| Enter text            | <kbd>enter</kbd>`importing`<kbd>enter</kbd>`parameter type string` |
| Exit insert-mode      | <kbd>esc</kbd>                                                     |

## Example-11

@
Extract method

``` abap
CLASS lcl_russian_peasant_multipl DEFINITION
  CREATE PUBLIC .
  
    PUBLIC SECTION.
        METHODS multiplication
          IMPORTING
            iv_left              TYPE i
            iv_right             TYPE i
            iv_write_calculation TYPE abap_bool DEFAULT abap_false
          RETURNING
            VALUE(rv_result)     TYPE i.

"...

ENDCLASS.

CLASS lcl_russian_peasant_multipl IMPLEMENTATION.

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

"...

ENDCLASS.
```

| WHAT                                             | HOW                                                                       |
|--------------------------------------------------|---------------------------------------------------------------------------|
| Search and jump to 'WHILE'                       | <kbd>/</kbd>`WHILE`<kbd>enter</kbd>                                       |
| One line down                                    | <kbd>j</kbd>                                                              |
| Line-selection                                   | <kbd>V</kbd>                                                              |
| 9 lines down / include next 9 lines in selection | <kbd>9</kbd><kbd>j</kbd>                                                  |
| Replace selection, moving it to register 'i'     | <kbd>"</kbd><kbd>i</kbd><kbd>c</kbd>                                      |
| Enter text                                       | `create_new_line( iv_left = iv_left iv_right = iv_right ).`<kbd>esc</kbd> |
| Jump to first non-blank character in line        | <kbd>^</kbd>                                                              |
| Select to end of word                            | <kbd>v</kbd><kbd>e</kbd>                                                  |
| Yank selection into register 'd'                 | <kbd>"</kbd><kbd>d</kbd><kbd>y</kbd>                                      |
| 8 lines down                                     | <kbd>8</kbd><kbd>j</kbd>                                                  |
| Insert new line below                            | <kbd>o</kbd>                                                              |
| Enter text                                       | `METHOD `<kbd>esc</kbd>                                                   |
| Paste content of register 'd'                    | <kbd>"</kbd><kbd>d</kbd><kbd>p</kbd>                                      |
| Insert '.' after cursor                          | <kbd>a</kbd>`.`<kbd>esc</kbd>                                             |
| Paste content of register 'i'                    | <kbd>"</kbd><kbd>i</kbd><kbd>p</kbd>                                      |
| 10 lines down                                    | <kbd>1</kbd><kbd>0</kbd><kbd>j</kbd>                                      |
| Insert new line below                            | <kbd>o</kbd>                                                              |
| Enter text                                       | `ENDMETHOD.`<kbd>esc</kbd>                                                |
| Backward-search to 'ENDCL'                       | <kbd>?</kbd>`ENDCL`<kbd>enter</kbd>                                       |
| Insert new line above                            | <kbd>O</kbd>                                                              |
| Enter text                                       | `METHOD `<kbd>esc</kbd>                                                   |
| Paste content of register 'd'                    | <kbd>"</kbd><kbd>d</kbd><kbd>p</kbd>                                      |
| 9 lines up                                       | <kbd>9</kbd><kbd>k</kbd>                                                  |
| Lines-selection                                  | <kbd>V</kbd>                                                              |
| 2 lines down / include next 2 lines in selection | <kbd>2</kbd><kbd>j</kbd>                                                  |
| Yank selection                                   | <kbd>y</kbd>                                                              |
| 9 lines down                                     | <kbd>9</kbd><kbd>j</kbd>                                                  |
| Paste                                            | <kbd>p</kbd>                                                              |
| Two lines down                                   | <kbd>2</kbd><kbd>j</kbd>                                                  |
| Insert '.' at end of line                        | <kbd>A</kbd>`.`<kbd>esc</kbd>                                             |



## Example-12

@
<Describe your Refactoring Goal>

``` abap
Code Snippet
..
Code Snippet
```

| WHAT                        | HOW                           |
|-----------------------------|-------------------------------|
| ...                         | ...                           |
| ...                         | ...                           |
| ...                         | ...                           |

## Example-13

@
<Describe your Refactoring Goal>

``` abap
Code Snippet
..
Code Snippet
```

| WHAT                        | HOW                           |
|-----------------------------|-------------------------------|
| ...                         | ...                           |
| ...                         | ...                           |
| ...                         | ...                           |

## Example-14

@
<Describe your Refactoring Goal>

``` abap
Code Snippet
..
Code Snippet
```

| WHAT                        | HOW                           |
|-----------------------------|-------------------------------|
| ...                         | ...                           |
| ...                         | ...                           |
| ...                         | ...                           |
Jump to @ sign, this is your vim-refactoring starting point.

