# تعطیلات رسمی ایران | Iran Holidays Calendar api

مجموعه داده‌های تعطیلات رسمی ایران بر اساس **تقویم هجری خورشیدی (شمسی)** در قالب JSON، مناسب برای استفاده در وب‌سایت‌ها، اپلیکیشن‌ها و پروژه‌های برنامه‌نویسی.

## ویژگی‌ها

- اطلاعات تعطیلات رسمی تقویم ایران
- ساختار ساده و قابل استفاده در زبان‌های برنامه‌نویسی مختلف
- مناسب برای تقویم‌های شمسی، سیستم‌های مدیریت و اپلیکیشن‌ها
- امکان استخراج و اضافه‌کردن تعطیلات سال‌های جدید

## اطلاعات موجود

فایل‌های JSON تعطیلات رسمی سال‌های مختلف تا سال **۱۴۰۱** در این مخزن قرار گرفته‌اند.

## دریافت تعطیلات سال‌های جدید از time.ir

برای دریافت تعطیلات رسمی سال‌های جدید، می‌توانید از وب‌سایت [Time.ir](https://www.time.ir/event-year) استفاده کنید.

### مراحل استخراج اطلاعات

1. وارد صفحه [تقویم سالانه Time.ir](https://www.time.ir/event-year) شوید.
2. سال موردنظر را انتخاب کنید.
3. کلید `F12` را فشار دهید و وارد بخش **Console** مرورگر شوید.
4. کد JavaScript زیر را اجرا کنید.
5. خروجی تعطیلات رسمی سال انتخاب‌شده به‌صورت خودکار در کلیپ‌بورد کپی می‌شود.

### کد استخراج تعطیلات رسمی

```javascript
const year = Number(document.querySelector("#year").value);

const holidays = [...document.querySelectorAll('[id^="Month_"]')]
    .flatMap(month => {
        const monthNumber = Number(month.id.split("_")[1]) + 1;

        return [...month.querySelectorAll('[class*="EventListItem-module"]')]
            .filter(item => item.querySelector('[class*="__date__holiday"]'))
            .map(item => ({
                year,
                month: monthNumber,
                day: Number(item.querySelector('[class*="__date"]').textContent.match(/\d+/)[0])
            }));
    });

const output = holidays
    .map(x => `\t{ year: ${x.year}, month: ${x.month}, day: ${x.day} },`)
    .join("\n");

console.log(output);
copy(output);
```

### نمونه خروجی

```javascript
{ year: 1408, month: 1, day: 1 },
{ year: 1408, month: 1, day: 2 },
{ year: 1408, month: 1, day: 3 },
```

خروجی شامل سه مقدار است:

| فیلد | توضیحات |
|---|---|
| `year` | سال شمسی |
| `month` | شماره ماه شمسی (۱ تا ۱۲) |
| `day` | روز ماه |

**توجه:** کد بالا تاریخ روزهای تعطیل را استخراج می‌کند و عنوان مناسبت‌ها را در خروجی قرار نمی‌دهد. همچنین در صورت تغییر ساختار HTML وب‌سایت Time.ir، ممکن است نیاز به به‌روزرسانی کد باشد.

## مشارکت در پروژه

اگر اطلاعات تعطیلات سال‌های جدید را استخراج کرده‌اید یا متوجه خطایی در داده‌ها شده‌اید، می‌توانید از طریق **Pull Request** یا **Issues** در تکمیل و اصلاح اطلاعات مشارکت کنید.

## منبع اطلاعات

[تقویم رسمی و مناسبت‌های ایران - Time.ir](https://www.time.ir/event-year)

---

### English

**Iran Holidays Calendar** provides Iranian official holiday dates based on the Solar Hijri (Jalali/Persian) calendar.

The repository contains holiday data in JSON format for use in websites, applications, and software projects.

Holiday data is currently included through the Persian calendar year **1401**.

To extract holiday dates for additional years, visit [Time.ir](https://www.time.ir/event-year), select the desired year, and run the JavaScript code above in your browser's developer console.

Contributions, corrections, and pull requests are welcome.
