I clicked activate license which prompted me to input a licence key and when I typed an invalid key it returned a popup saying `Invalid Licence Key`.

I searched for `Invalid Licence Key` and found three code references and clicked on the first one which lead me to the method `0x421c50`.

```c
00421c50    int32_t __fastcall sub_421c50(char* arg1, int32_t* arg2)

00421c50    {
00421c50        int32_t var_8 = 0xffffffff;
00421c55        int32_t (* var_c)(void* arg1) = sub_8f9ef8;
00421c60        TEB* fsbase;
00421c60        struct _EXCEPTION_REGISTRATION_RECORD* ExceptionList = fsbase->NtTib.ExceptionList;
00421c69        int32_t __saved_ebp;
00421c69        int32_t eax_2 = __security_cookie ^ &__saved_ebp;
00421c71        int32_t var_44 = eax_2;
00421c75        fsbase->NtTib.ExceptionList = &ExceptionList;
00421c88        sub_40d1c0(arg2, "Invalid Licence Key", 0x13);
00421ca3        char var_34;
00421ca3        int32_t result;
00421ca3        
00421ca3        if (!sub_421b20(&var_34, arg1) || var_34 != 0x7c)
00421d59            result = 0;
00421ca3        else
00421ca3        {
00421caf            int32_t* var_2c;
00421caf            sub_421850(&var_2c, &var_34);
00421cb4            int32_t var_8_1 = 0;
00421cbb            int32_t* eax_4 = &var_2c;
00421cc3            int32_t var_18;
00421cc3            
00421cc3            if (var_18 >= 0x10)
00421cc3                eax_4 = var_2c;
00421cc3            
00421cd2            if (sub_8c5285(eax_4, arg1))
00421cd2            {
00421d2f                if (var_18 >= 0x10)
00421d2f                {
00421d31                    int32_t* ecx_5 = var_2c;
00421d34                    int32_t edx_7 = var_18 + 1;
00421d35                    int32_t* eax_9 = ecx_5;
00421d35                    
00421d3d                    if (edx_7 >= 0x1000)
00421d3d                    {
00421d3f                        ecx_5 = ecx_5[-1];
00421d42                        edx_7 += 0x23;
00421d42                        
00421d4d                        if ((char*)eax_9 - ecx_5 - 4 > 0x1f)
00421d4d                        {
00421d7c                            sub_8b6e5f();
00421d7c                            /* no return */
00421d4d                        }
00421d3d                    }
00421d3d                    
00421d4f                    int32_t var_48_4 = edx_7;
00421d51                    sub_6e48e6(ecx_5);
00421d2f                }
00421d2f                
00421d59                result = 0;
00421cd2            }
00421cd2            else
00421cd2            {
00421cd4                char* edx_2 = arg1;
00421ce5                uint32_t eax_5;
00421ce5                
00421ce5                do
00421ce5                {
00421ce0                    (uint8_t)eax_5 = *(uint8_t*)edx_2;
00421ce2                    edx_2 = &edx_2[1];
00421ce5                } while ((uint8_t)eax_5);
00421ced                sub_40d1c0(arg2, arg1, edx_2 - &edx_2[1]);
00421ced                
00421cf8                if (var_18 >= 0x10)
00421cf8                {
00421cfa                    int32_t* ecx_4 = var_2c;
00421cfd                    int32_t edx_5 = var_18 + 1;
00421cfe                    int32_t* eax_6 = ecx_4;
00421cfe                    
00421d06                    if (edx_5 >= 0x1000)
00421d06                    {
00421d08                        ecx_4 = ecx_4[-1];
00421d0b                        edx_5 += 0x23;
00421d0b                        
00421d16                        if ((char*)eax_6 - ecx_4 - 4 > 0x1f)
00421d16                        {
00421d77                            sub_8b6e5f();
00421d77                            /* no return */
00421d16                        }
00421d06                    }
00421d06                    
00421d18                    int32_t var_48_3 = edx_5;
00421d1a                    sub_6e48e6(ecx_4);
00421cf8                }
00421cf8                
00421d22                result = 1;
00421cd2            }
00421ca3        }
00421ca3        
00421d5e        fsbase->NtTib.ExceptionList = ExceptionList;
00421d6e        sub_6e48d5(eax_2 ^ &__saved_ebp);
00421d76        return result;
00421c50    }
```

This method returns a boolean which I assumed to be a licence check so I patched it to always return true.

```c
00421c50    int32_t sub_421c50() __pure

00421c50    {
00421c50        return 1;
00421c50    }
```

I scrolled down to the next method after `0x421c50` and found the method `0x421d90`.
```c
00421d90    int32_t sub_421d90()

00421d90    {
00421d90        int32_t var_8 = 0xffffffff;
00421d95        int32_t (* var_c)(void* arg1) = sub_8fa951;
00421da0        TEB* fsbase;
00421da0        struct _EXCEPTION_REGISTRATION_RECORD* ExceptionList = fsbase->NtTib.ExceptionList;
00421da9        int32_t __saved_ebp;
00421da9        int32_t eax_2 = __security_cookie ^ &__saved_ebp;
00421db0        int32_t var_54 = eax_2;
00421db4        fsbase->NtTib.ExceptionList = &ExceptionList;
00421dbc        int32_t var_48 = 0;
00421dc3        int32_t var_1c = 0;
00421dca        int32_t var_18 = 0xf;
00421dd1        char var_2c = 0;
00421dd8        int32_t var_8_1 = 0;
00421ddf        void* var_44;
00421ddf        int32_t* eax_3 = sub_422330(&var_44);
00421de4        (uint8_t)var_8_1 = 1;
00421dec        int32_t var_48_1 = 1;
00421dec        
00421df3        if (eax_3[5] >= 0x10)
00421df5            eax_3 = *(uint32_t*)eax_3;
00421df5        
00421dfa        char* var_58 = &var_2c;
00421e0a        int32_t ebx;
00421e0a        
00421e0a        if (!sub_425580(&var_2c, eax_3) || !var_1c)
00421e10            (uint8_t)ebx = 0;
00421e0a        else
00421e0c            (uint8_t)ebx = 1;
00421e0c        
00421e12        int32_t var_8_2 = 0;
00421e1f        int32_t var_30;
00421e1f        
00421e4b        int32_t result;
00421e4b        result = !(uint8_t)ebx ? 0 : 1;
00421e4b        
00421e9a        fsbase->NtTib.ExceptionList = ExceptionList;
00421ea9        sub_6e48d5(eax_2 ^ &__saved_ebp);
00421eb1        return result;
00421d90    }
```

Which returned a boolean and had three cross references, making me believe that it was another valid licence check, so I patched it to always return true.

```c
00421d90    int32_t sub_421d90() __pure

00421d90    {
00421d90        return 1;
00421d90    }
```

My apologies if I was very vague on this one; I got pretty lucky with my guesswork, and surprisingly, it didn't take too long.

HTTP Debugger installer is available from the [HTTP Debugger Website](https://www.httpdebugger.com/download).