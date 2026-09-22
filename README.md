#define u32     unsigned int
#define RCC_APB2ENR     (*(volatile u32 *)0x40021018)

#define GPIOA_CRL       (*(volatile u32 *)0x40010800)
#define GPIOA_ODR       (*(volatile u32 *)0x4001080C)

#define GPIOB_CRL       (*(volatile u32 *)0x40010C00)
#define GPIOB_ODR       (*(volatile u32 *)0x40010C0C)

#define GPIOC_CRH       (*(volatile u32 *)0x40011004)
#define GPIOC_ODR       (*(volatile u32 *)0x4001100C)

#define DELAY_COUNT     4000000
void Delay(void)
{
    u32 i = 0;
    for (i = 0; i < DELAY_COUNT; i++)   /* ???,??????? */
    {
        ;
    }
}

int main(void)
{

    RCC_APB2ENR |= (1 << 2) | (1 << 3) | (1 << 4);
 
    GPIOA_CRL &= 0xFFF0FFFF;        
    GPIOA_CRL |= 0x00020000;     
  
    GPIOB_CRL &= 0xFF0FFFFF;        
    GPIOB_CRL |= 0x00200000;        
    GPIOC_CRH &= 0xFF0FFFFF;     
    GPIOC_CRH |= 0x00200000;      

    GPIOA_ODR &= ~(1 << 4);         
    GPIOB_ODR &= ~(1 << 5);        
    GPIOC_ODR &= ~(1 << 13);       
   
    while (1)
    {
 
        GPIOA_ODR |=  (1 << 4);        
        GPIOB_ODR &= ~(1 << 5);       
        GPIOC_ODR &= ~(1 << 13);        
        Delay();                        
     
        GPIOA_ODR &= ~(1 << 4);
        GPIOB_ODR |=  (1 << 5);
        GPIOC_ODR &= ~(1 << 13);
        Delay();
 
        GPIOA_ODR &= ~(1 << 4);
        GPIOB_ODR &= ~(1 << 5);
        GPIOC_ODR |=  (1 << 13);
        Delay();
    }
}
}
