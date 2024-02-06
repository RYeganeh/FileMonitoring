---
# __پروژه میانترم سیستم عامل__
### __file monitoring,Linux NCDU simulator__

---
>فایل زیپ تحویل داده شده پروژه شامل دو فایل است.
یک فایل مربوط به برنامه پروژه بدون رابط گرافیکی است که از طریق چاپ فایل ها و فولدر های یافته شده در ترمینال، ایجاد حالت موازی رشته ها مشهود می گردد.
فایل دیگر نیز مربوط به برنامه پروژه با رابط کاربری گرافیکی است که انتخاب فولدر مدنظر و نمایش نتایج از طریق پنجره گرافیکی خواهد بود.

>>### __۱) midterm_project.c__
>>این فایل علاوه بر تابع main حاوی توابع child_proccesses و count_file نیز هست.
در ابتدا مقادیری که باید به عنوان نتیجه چاپ شود را به صورت یک استراکچر تعریف می کنیم. این مقادیر را در تابع main مقدار دهی اولیه می کنیم و پس از آنکه کاربر آدرس فولدر مدنظر خود را وارد کرد، تابع child_processes را صدا می زنیم و آدرس را به عنوان آرگومان ارسال می کنیم.
>>> + __child_processes:__
>>> در این تابع فایل ها و فولدر های سطح اول فولدر ریشه را بررسی می کنیم. به ازای هر فولدر، فرایند اصلی یک فرزند fork می کند. این فرزند برای بررسی فولدری که در اختیارش قرار داده شده است از رشته ها استفاده می کند. هر فرآیند فرزند بعد از بررسی فولدر تحت اختیارش از بین می رود. از آنجا که فرزند ها بررسی هایشان در فولدر هایی مجزایی انجام می دهند، کارهایشان و نتایجی که به دست می آورند با یکدیگر تداخل ندارد. به همین علت برای برقراری ارتباط میان فرآیند های فرزند و والد از حافظه مشترک استفاده  شده است.
فرآیندهای فرزند برای ورود به سطح بعدی در فولدرهایشان تابع count_file را فراخوانی می کنند.

>>> + __count_file:__
>>> در این تابع نیز مانند تابع قبل فایل ها و فولدر ها را سطحی که در آن واقع هستیم بررسی می کنیم. تفاوت این سطوح با  سطح اول در این است که پس از شناسایی هر فولدر برای دوباره صدا زدن این تابع از رشته ها استفاده می کنیم نه فرآیند ها. بدین صورت که تابع count_file را برای سطح بعد با استفاده از نخ ها فراخوانی می کنیم تفاوت این حالت با فواخوانی عادی این تابع در این است که توابع به صورت موازی فراخوانی می شوند برای مشخص شدن حالت موازی نخ ها، پس از یافته شدن هر فایل یا فولدر، اسم آن در ترمینال به علاوه tid رشته ای که فایل را پیدا کرده است چاپ می شود.

>> در انتها مقادیر ذخیره شده در استراکچر که شامل اطلاعات به دست آمده از فولدر مد نظر است در تابع main چاپ می شوند.


>>### __۲) midterm_project_GUI:__
>>رابط کاربری گرافیکی در برنامه با استفاده از کتابخانه <gtk/gtk.h> پیاده سازی شده است.
در این برنامه علاوه بر توابع برنامه قبل، تابع on_button_clicked نیز افزوده شده است.
در این برنامه، داخل تابع main موارد مربوط به پیاده سازی اولیه پنجره گرافیکی قرار داده شده است.
>>> + __on_button_clicked:__
>>> در این تابع ابتدا مقدار دهی های اولیه نتایج که به صورت استراکچر تعریف شده اند انجام میشود.
با کلیک کردن کاربر بر روی کلید انتخاب فولدر، پنجره ای باز می شود که شامل تمامی فولدر های موجود در سیستم است. کاربر فولدر مد نظر خود را انتخاب می کند. آدرس به دست آمده به تابع child_processes ارسال می شود. سپس نتایج مدنظر داخل یک label چاپ می شود.
بعد از چاپ اطلاعات، این برنامه تمام نمی شود و از آنجا که مقدار دهی های اولیه در این تابع انجام می شود، کاربر می تواند دوباره یک مسیر دیگر را انتخاب کند و اطلاعات مدنظر خود را مشاهده کند.
اگر پیش از انتخاب مسیر دوم، تغییراتی در فایل های سیستم به وجود آوریم، با باز کردن دوباره پنجره حاوی تمام فولدر های سیستم، مشاهده می کنیم که این تغییرات اعمال شده است.