# ILI93XX LCD driver

The library represents minimal hardware independent driver for "ILI93XX" LCD controller 
for testing and education purposes.

It requires low-level register operation implementation and provides the following functionality:

- LCD initialization
- filling rectangle with a specified color
- filling rectangle from buffer

Supported ILI93XX models:

- ILI9320
- ILI9325
- ILI9328
- ILI9331

## Basic usage

```
// Create and clear driver
lcd_ili93xx_driver_t lcd_driver;
lcd_ili93xx_init_clear(&lcd_driver);

// Attach callbacks to handler:
// set custom data. If don't need any data, assign NULL.
lcd_driver.user_data = my_data_ptr;
// Set delay callback (it's needed for LCD initialization)
lcd_driver.delay = my_delay;
// Set callback that resets LCD.
lcd_driver.reset = my_lcd_reset_callback;
// Set callback that can write a single value to register.
lcd_driver.write_reg = my_lcd_write_reg;
// Set callback that can read a single value from register.
lcd_driver.read_reg = my_lcd_read_reg;
// Set callback that can write multiple word to register.
lcd_driver.write_words = my_lcd_write_words;

// Initialize driver:
int res = lcd_ili93xx_init(&lcd_driver);
if (!res) {
    // Driver initialization error.
    // Show error somehow and stop application
    // ...
}

// Use driver for some operations.
lcd_ili93xx_fill_rect_color(&lcd_driver, 0, 0, 240, 320, LCD_ILI93XX_COLOR_GREEN);
```
