I clicked activate license which prompted me to input a licence key and when I typed an invalid key it returned a popup saying `Invalid Licence Key`.

I searched for `Invalid Licence Key` and found three code references and clicked on the first one which lead me to the method `0x459540`.

```c
00459540    int32_t __fastcall sub_459540(char* arg1, int32_t* arg2)

00459540    {
00459540        int32_t var_8 = 0xffffffff;
00459545        int32_t (* var_c)(void* arg1) = sub_a0eeb8;
00459550        TEB* fsbase;
00459550        struct _EXCEPTION_REGISTRATION_RECORD* ExceptionList = fsbase->NtTib.ExceptionList;
00459559        int32_t __saved_ebp;
00459559        int32_t eax_2 = __security_cookie ^ &__saved_ebp;
00459561        int32_t var_44 = eax_2;
00459565        fsbase->NtTib.ExceptionList = &ExceptionList;
00459578        sub_413550(arg2, "Invalid Licence Key", 0x13);
00459593        char var_34;
00459593        int32_t result;
00459593        
00459593        if (!sub_459410(&var_34, arg1) || var_34 != 0x7c)
00459649            result = 0;
00459593        else
00459593        {
0045959f            int32_t* var_2c;
0045959f            sub_4590c0(&var_2c, &var_34);
004595a4            int32_t var_8_1 = 0;
004595ab            int32_t* eax_4 = &var_2c;
004595b3            int32_t var_18;
004595b3            
004595b3            if (var_18 >= 0x10)
004595b3                eax_4 = var_2c;
004595b3            
004595c2            if (__stricmp(eax_4, arg1))
004595c2            {
0045961f                if (var_18 >= 0x10)
0045961f                {
00459621                    int32_t* ecx_5 = var_2c;
00459624                    int32_t edx_7 = var_18 + 1;
00459625                    int32_t* eax_9 = ecx_5;
00459625                    
0045962d                    if (edx_7 >= 0x1000)
0045962d                    {
0045962f                        ecx_5 = ecx_5[-1];
00459632                        edx_7 += 0x23;
00459632                        
0045963d                        if ((char*)eax_9 - ecx_5 - 4 > 0x1f)
0045963d                        {
0045966c                            __invalid_parameter_noinfo_noreturn();
0045966c                            /* no return */
0045963d                        }
0045962d                    }
0045962d                    
0045963f                    int32_t var_48_4 = edx_7;
00459641                    sub_7af956(ecx_5);
0045961f                }
0045961f                
00459649                result = 0;
004595c2            }
004595c2            else
004595c2            {
004595c4                char* edx_2 = arg1;
004595d5                uint32_t eax_5;
004595d5                
004595d5                do
004595d5                {
004595d0                    (uint8_t)eax_5 = *(uint8_t*)edx_2;
004595d2                    edx_2 = &edx_2[1];
004595d5                } while ((uint8_t)eax_5);
004595dd                sub_413550(arg2, arg1, edx_2 - &edx_2[1]);
004595dd                
004595e8                if (var_18 >= 0x10)
004595e8                {
004595ea                    int32_t* ecx_4 = var_2c;
004595ed                    int32_t edx_5 = var_18 + 1;
004595ee                    int32_t* eax_6 = ecx_4;
004595ee                    
004595f6                    if (edx_5 >= 0x1000)
004595f6                    {
004595f8                        ecx_4 = ecx_4[-1];
004595fb                        edx_5 += 0x23;
004595fb                        
00459606                        if ((char*)eax_6 - ecx_4 - 4 > 0x1f)
00459606                        {
00459667                            __invalid_parameter_noinfo_noreturn();
00459667                            /* no return */
00459606                        }
004595f6                    }
004595f6                    
00459608                    int32_t var_48_3 = edx_5;
0045960a                    sub_7af956(ecx_4);
004595e8                }
004595e8                
00459612                result = 1;
004595c2            }
00459593        }
00459593        
0045964e        fsbase->NtTib.ExceptionList = ExceptionList;
0045965e        sub_7af945(eax_2 ^ &__saved_ebp);
00459666        return result;
00459540    }
```

This method returns a boolean which I assumed to be a licence check so I patched it to always return true.

```c
00459540    int32_t sub_459540() __pure

00459540    {
00459540        return 1;
00459540    }
```

I scrolled down to the next method after `0x459540` and found the method `0x459680`.
```c
00459680    int32_t sub_459680()

00459680    {
00459680        int32_t var_8 = 0xffffffff;
00459685        int32_t (* var_c)(void* arg1) = sub_a12571;
00459690        TEB* fsbase;
00459690        struct _EXCEPTION_REGISTRATION_RECORD* ExceptionList = fsbase->NtTib.ExceptionList;
00459699        int32_t __saved_ebp;
00459699        int32_t eax_2 = __security_cookie ^ &__saved_ebp;
004596a0        int32_t var_54 = eax_2;
004596a4        fsbase->NtTib.ExceptionList = &ExceptionList;
004596ac        int32_t var_48 = 0;
004596b3        int32_t var_1c = 0;
004596ba        int32_t var_18 = 0xf;
004596c1        char var_2c = 0;
004596c8        int32_t var_8_1 = 0;
004596cf        void* var_44;
004596cf        int32_t* eax_3 = sub_459c20(&var_44);
004596d4        (uint8_t)var_8_1 = 1;
004596dc        int32_t var_48_1 = 1;
004596dc        
004596e3        if (eax_3[5] >= 0x10)
004596e5            eax_3 = *(uint32_t*)eax_3;
004596e5        
004596ea        char* var_58 = &var_2c;
004596fa        int32_t ebx;
004596fa        
004596fa        if (!sub_45fc80(&var_2c, eax_3) || !var_1c)
00459700            (uint8_t)ebx = 0;
004596fa        else
004596fc            (uint8_t)ebx = 1;
004596fc        
00459702        int32_t var_8_2 = 0;
0045970f        int32_t var_30;
0045970f        
0045970f        if (var_30 >= 0x10)
0045970f        {
00459711            void* ecx_2 = var_44;
00459714            int32_t edx_1 = var_30 + 1;
00459715            void* eax_5 = ecx_2;
00459715            
0045971d            if (edx_1 >= 0x1000)
0045971d            {
0045971f                ecx_2 = *(uint32_t*)((char*)ecx_2 - 4);
00459722                edx_1 += 0x23;
00459722                
0045972d                if ((char*)eax_5 - ecx_2 - 4 > 0x1f)
0045972d                {
004597a2                    __invalid_parameter_noinfo_noreturn();
004597a2                    /* no return */
0045972d                }
0045971d            }
0045971d            
0045972f            int32_t var_58_1 = edx_1;
00459731            sub_7af956(ecx_2);
0045970f        }
0045970f        
0045973b        int32_t result;
0045973b        
0045973b        result = !(uint8_t)ebx ? 0 : 1;
0045973b        
0045975b        if (var_18 >= 0x10)
0045975b        {
0045975d            void* ecx_4 = var_2c;
00459760            int32_t edx_4 = var_18 + 1;
00459761            void* eax_8 = ecx_4;
00459761            
00459769            if (edx_4 >= 0x1000)
00459769            {
0045976b                ecx_4 = *(uint32_t*)((char*)ecx_4 - 4);
0045976e                edx_4 += 0x23;
0045976e                
00459779                if ((char*)eax_8 - ecx_4 - 4 > 0x1f)
00459779                {
004597a7                    __invalid_parameter_noinfo_noreturn();
004597a7                    /* no return */
00459779                }
00459769            }
00459769            
0045977b            int32_t var_58_2 = edx_4;
0045977d            sub_7af956(ecx_4);
0045975b        }
0045975b        
0045978a        fsbase->NtTib.ExceptionList = ExceptionList;
00459799        sub_7af945(eax_2 ^ &__saved_ebp);
004597a1        return result;
00459680    }
```

Which returned a boolean and had three cross references, making me believe that it was another valid licence check, so I patched it to always return true.

```c
00459680    int32_t sub_459680() __pure

00459680    {
00459680        return 1;
00459680    }
```

My apologies if I was very vague on this one; I got pretty lucky with my guesswork, and surprisingly, it didn't take too long.

This is basically a copy and paste of 9.12, updated for 10.9. I'm unable to test if this works until the trial is over, but I'm assuming it will due to the code structures being the same

HTTP Debugger installer is available from the [HTTP Debugger Website](https://www.httpdebugger.com/download).