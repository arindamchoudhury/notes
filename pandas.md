df.info()
df.shape
df.columns

df.head()
df.tail()

## remove duplicates
df_cleaned = df[~df.duplicated()]
df.duplicated(subset=['brand'])
## filter/remove rows
bad_product_price = df_cleaned["prod_price"] == 8675309
df_cleaned = df_cleaned[~bad_product_price]

## change column value based on some logic
df_cleaned.loc[df["cust_state"] == "AL", "cust_state"] = "Alabama"

## get sorted distict values for a column
sorted(df_cleaned["cust_state"].unique())

## get total number of null values
df_cleaned.isna().sum().sum()

## drop a column
df_cleaned.drop('prod_size', axis=1, inplace=True)

## group by
df.groupby("subscriptionTier")["totalcost"].mean()
df.groupby("subscriptionTier")[["totalcost", "monthlybaseprice"]].mean()
df.groupby("subscriptionTier")["totalcost"].agg(["sum", "mean", "max", "min", "count"])

## column statistics
df["subscriptionTier"].value_counts()                   # gives counts
df["subscriptionTier"].value_counts(normalize=True)     # gives percentage

df["monthlybaseprice"].quantile(0.75)


## get top values for a column(prod_title) based on column(trans_quantity)
df_cleaned.groupby("prod_title")["trans_quantity"].sum().sort_values(ascending=False).head(10).to_frame().reset_index()["prod_title"]


# get values from row as tuple
df_cleaned[['trans_month','trans_day']].apply(tuple, axis=1).iloc[0]
df_cleaned[['trans_month','trans_day']].apply(tuple, axis=1).iloc[-1]

# get specific row where column(prod_animal_type) value is high
most_pop = tuple(zip(df_cleaned["prod_animal_type"].value_counts(normalize=True).sort_values(ascending=False).head(1).to_frame().reset_index()["index"]))[0][0]

