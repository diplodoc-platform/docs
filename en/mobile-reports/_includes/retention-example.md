- Date range is December 1 — March 24.
- Grouping by sources is enabled.
- The time range is divided into months.
- Retention metrics is selected.

![](../../../_images/retention-group-by-source-{{ locale }}.png){style="border: solid 1px #cccccc; max-width: 800px;"}

Example of calculating the percentage of users who returned in the first month after installation:

$$ \frac{353}{2814} × 100 = 12.54 $$

The report displays 17.20%. The resulting numbers differ because the interface displays the number of all returned users grouped by the partner, and the percentage of returns is calculated only for the completed time interval.

![](../../../_images/retention-group-by-date-{{ locale }}.png){style="border: solid 1px #cccccc; max-width: 800px;"}

For example, it's the 24 of March. For installations made in February, the first month (March) is not over yet. So February is not included into the calculation of the final value of the first month. Therefore, to calculate the percentage of returns in the first month, you need to sum only the values of the zero months, which values are taken into account.

To calculate the percentage of returned users in the first month:

1. Turn on grouping by installation date.
2. Enable segmentation by the appropriate installation source.
3. Divide the total number of returned users in the first month by the total number of installations in July and August:

   $$ \frac{147 + 107}{747 + 734} × 100 = 17.15 $$

   In the report, the value of 17.15 is rounded to a decimal place: 17.20%.
   