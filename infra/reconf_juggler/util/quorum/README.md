# NAME

quorum - Quorum calculator

# SYNOPSIS

    quorum [OPTIONS] <arguments>

# DESCRIPTION

Calculate quorum and hysteresis for passed values

## Output fields

- **INPUT** Input value
- **QPERC** Quorum, percents
- **QABST** Quorum, absolute
- **QPRCI** Quorum, inverted percents
- **QABSI** Quorum, inverted absolute
- **HPERC** Hysteresis, percents
- **HABST** Hysteresis, absolute

# OPTIONS

- **-d, --dump**

    Calculate nothing, just dump used table.

- **-f, --fields** LIST

    Comma separated fields to show.

- **-j, --json**

    Print result as JSON.

- **-h, --help**

    Print help message and exit.

- **-q, --quiet**

    Don't print headers. Meaningless in --json mode.

- **-t, --table** NAME

    Which table to use. Load from file if file exists or use builtin one
    otherwise. There are 99..50 builtin tables available; table name indicates
    absolute quorum on input 100 (mimicking percent for convenience).

    `90` table is used by default.

- **-V, --version**

    Print version and exit.

# EXAMPLES

Show quorums for values 13, 42 and 67:

    quorum 13 42 67

Same as above, but as JSON:

    quorum --json 13 42 67

Use another table from standard set:

    quorum --table 93 -- 13 42 67

Use third-part table:

    quorum --table ./my_quorums.json 13 42 67

Print INPUT and QABSI only:

    quorum --fields INPUT,QABSI 13 42 67
