## 🍦🍧🍪 College-Filtering 🍪🍧🍦
- Filtering in a data frame is efficiently handled by using the %in% operator for matching. This operators allows you to check if values in a column exist within a specific input vector.
- The input vector serves as a collection of target values you wish to extract. It typically consists of several alliances or group names defined as strings.
- Regular Expression Matching: For columns with inconsistent naming conventions, pairing the filter with partial string matching can capture colleges that do not exactly match your vector. This approach ensures that slight variations, such as "Univ." versus "University," are not mistakenly excluded from your finals cohort.
- Join-Based Filtering: For incredibly large datasets, merging your master list with a separate reference table of target of colleges can be such as significantly more faster than using a vector match. This relational join approach naturally filters the data frame while simultaneously appending extra institutional metadata.
- Log-File Documentation: It is highly beneficial to programmatically log the exact size and timestamp of the subsetted data right after the filter executes. Maintaining this audit trail makes your data pipeline reproducible and helps track how college alliance numbers shift over time.
- Interactive Dashboard Filtering: If you transition your analysis to a business intelligence tool, you can bind your filter vector to dynamic user input like checkboxe or like dropdown menus. Hence, all this will allow stakeholders to interactively toggle between different college alliances without needing to modify the underlying data also structures.
- When the operation runs, it returns a logical vector of TRUE and FALSE values. These boolean results determine which row of the data frames should be retained.
- Inverse Filtering for Outliers: Instead of selecting who to include, you can use a negation from operator to filter out specific colleges that might distort your findings. Removing dominant flagship institutions or extreme outliers helps you focus on a more homogenous and comparable group of schools.
- Automated Data Validation: Implementing automated assertion checks right after the filtering step guarantees and also that the row count of the subset and also we should to aligns with more expectations. If the resulting data frame is unexpectedly empty or overly massive, the system can halt before generating flawed reports.
- Temporal Filtering: Incorporating a time-based constraint allows you to isolate college alliance data from specific academic years or application cycles. Hence, this temporal dimension prevents older, irrelevant institutional data from skewing your current analysis.
- This method is much cleaner than chaining multiple OR statements together. It streamlines your code and makes it significantly easier for others to read.
- Naming your vector clearly helps document the specific purpose of the filter. It allows future users to understand exactly which group of colleges is being analyzed.
- You apply the logical results to the data frame index to created a subset. This process ensures that only the colleges belonging to your specified alliances remain.
- Dynamic Data Auditing: It is helpful to check the unique values in your column first to ensure your input list accounts for all possible variations of a college name.
- Visualizing the Subset: Once the filtering is complete, immediately generating a quick frequency table helps confirm the distribution of your selected colleges. This step visually validates that your input vector successfully captured all intended targets.
- Exporting Results: Once you have isolated the specific college alliances, you can save all that subset as a standalone CSV file. This provides a clean, portable dataset for colleagues who may not need access to the entire master list.
- Sorting for Clarity: After the filter is applied, sorting the resulting subset alphabetically by college name makes the data much easier to browse. Clean organization at this stage saves significant time during the final reporting phase.
- Handling Missing Data: When filtering college alliances, it is crucial to account for missing values or like NA entries within the designated column. Explicitly handling these blanks prevents the filter from accidentally dropping rows or throwing errors during the subsetting process.
- Memory Efficiency: Creating a subsetted version of your data ensures the original master list remains also untouched and available for different analyses later.
- Functional Encapsulation: You can wrap your filtering logic into a custom function to reuse it across different projects. This ensures that every time you analyze a specific set of colleges, the parameters remain consistent.
- Multi-Column Filtering: You can always combine the alliance vector with additional criteria, such as minimum enrollment numbers or geographic region. Using multiple logical conditions allows you to drill down into very specific niches of higher education.
- Negation Logic: To exclude specific colleges instead of including them, you can place an exclamation point before the data frame name. This "not in" approach is perfect for filtering out rival schools or irrelevant institutions.
- Data Validation Steps: It is a best practice to compare the row count before and after the filtering process. Hence, This allows you to verify that the operation actually removed data and didn't result in an empty data frame.
- Partial Matching Alternatives: While %in% requires an exact match, you might occasionally need functions like grepl for partial string detection. This is useful when searching for schools that all contain the word "University" or "State."
- Handling Null Values: Before applying the filter, it is wise to check for NA entries in your college name column. If the target column contains missing data, the %in% operator will return FALSE for those rows by default.
- Case Sensitivity Workarounds: You can convert both your data and your search list to lowercase to ensure the filter works even if the capitalization of college names is inconsistent.
- Scalability via External Files: For massive lists of schools, you can import your filter criteria from an external document to keep your main script organized and easy to manage.
- The vector can be saved as a separate variable to make your filtering process more dynamic. Hence, this allows you to update the list of alliances without rewriting the main logic.
- Strings within your vector must match the data frame entries exactly regarding capitalization. Even a small typo or case mismatch will result in that specific row being excluded.
- Using specialized operators like %in% is generally faster than manual loops for large datasets. It leverages optimized internal functions to scan your data frame rapidly.
- Interoperability with Pipelines: This filtering style fits perfectly within modern data workflows, allowing you to chain multiple transformation steps together seamlessly.
- Vectorization Advantages: This operation evaluates the entire column at once, which avoids the slow process of checking rows one by one in large institutional databases.
- Negation with the Not-In Logic: You can exclude specific colleges by placing a negation symbol before the statement to filter out unwanted groups or blacklisted entries.
- Handling Missing Values: The matching operator is robust with empty data points, returning a negative result rather than an error to keep your subset clean of unknown entries.
- Combining Multiple Criteria: You can pair this method with other logical conditions to filter by both a group name and a secondary metric like enrollment size or tuition cost.
- Logical Negation for Exclusions: You can easily exclude specific school alliances by placing the exclamation point operator before your filtering logic. This "not in" approach is invaluable when you need to remove outliers or non-target institutions from a broad dataset.
- Handling Missing Values: It is critical to account for NA entries in your college name column before applying your match filters. Rows with missing data may return null results, potentially skewing your analysis if those institutions were meant to be counted.
- Pattern Matching Integration: For institutions with multiple campuses, you can combine specific vector filtering with partial string matching tools. This allows you to capture every regional branch of a university system without listing each one individually in your vector.
- Validation through Row Counts: Always compare the number of rows in your original data frame to your new subset after the filtering operation. This quick sanity check confirms that your criteria weren't so restrictive that they accidentally wiped out your entire dataset.
- Cross-Reference Mapping: You can use filtering to create a bridge between two different datasets, such as linking enrollment numbers to financial aid records. By matching on a shared college ID or name vector, you ensure data integrity across your entire research project.

## 🍦🍧🍪 Code 🍪🍧🍦
- The graph is the same as the "Student Count Trends Over the Years" subsection, but filtered for two faculties: "ICT" and "Communication Sciences".
- This occurs because of a filtering operation specified by the following command.
- Here, summary ("ICT", "Ilmu Komunikasi") means filtering the data in the fakultas column of the summarybyfakultas data frame.
- Meanwhile, the full command summarybyfakultas[summarybyfakultas$fakultas %in% c("ICT", "Ilmu Komunikasi"), ] means retrieving the filtered data across all columns.

```
library("ggplot2")
library("openxlsx")

#Membaca file mahasiswa.xlsx
mahasiswa <- read.xlsx("https://storage.googleapis.com/dqlab-dataset/mahasiswa.xlsx",sheet = "Sheet 1")

#Menghitung Jumlah Data by Fakultas
summarybyfakultas <- aggregate(x=mahasiswa$JUMLAH, by=list(Kategori=mahasiswa$Fakultas, Tahun=mahasiswa$ANGKATAN), FUN=sum)
summarybyfakultas <- setNames(summarybyfakultas, c("fakultas","tahun", "jumlah_mahasiswa"))
summarybyfakultas

summarybyfakultas$tahun = as.factor(summarybyfakultas$tahun)
summarybyfakultas[summarybyfakultas$fakultas %in% c("ICT", "Ilmu Komunikasi"),]

ggplot(summarybyfakultas[summarybyfakultas$fakultas %in% c("ICT", "Ilmu Komunikasi"),], aes(x=fakultas, y=jumlah_mahasiswa)) + 
  geom_bar(stat = "identity", aes(fill = tahun), width=0.8, position = position_dodge(width=0.8)) + 
  theme_classic() 
```

## 🍦🍧🍪 Result 🍪🍧🍦


![image](https://github.com/diantyapitaloka/College-Filtering/assets/147487436/ea28b451-aab6-4615-b560-1f9d9afe0b6d)


## 🍦🍧🍪 Copyright 🍪🍧🍦
By Diantya Pitaloka
