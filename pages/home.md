---
name: Home
assetId: 986c49ba-9c08-4f2c-bf1f-f6e8e796ca1a
type: page
---

# Welcome

# Filter nach `sortnumber` (Preisstufe)

{% dropdown
    id="x10_filter"
    data="x10_table"
    value_column="sortnumber"
    title="Sortnumber"
    multiple=true
/%}
```sql x10_table
select
cast(sortnumber as VARCHAR) as sortnumber, dimension, tariff_47012, tariff_48000, tariff_48004, tariff_48008, tariff_48012, tariff_49000, tariff_49004, tariff_50000 
from databricks_x10_tickets_long_by_tariff
order by 1, 2
```

{% table
    data="x10_table"
    filters=["x10_filter"]
%}
{% /table %}

```sql x10_bar
select tariff_49000 as name from databricks_x10_tickets_long_by_tariff 
where dimension = 'article_shortname'
```

# Anzahl nach Artikelname für Tarif 49000

{% bar_chart
    data="x10_bar"
    x="name"
    y="count(*)"
    order="count(*) desc"
    x_axis_options={
        label_rotate=90
    }
/%}