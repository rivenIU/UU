#### 加密强随机数 SecureRandom

[原文链接](https://wretchant.blog.csdn.net/article/details/84953724)

1、SecureRandom 应用场景

    第一个，由于当种子相同的时候，生成的随机数完全相同
    第二个，当随机数生成量较大时，Random存在性能问题
    所以，当需要大量随机数且对随机数安全性有要求的时候，使用SecureRandom更为合适

2、如何创建 SecureRandom 实例

    SecureRandom secureRandom = new SecureRandom();
    
    SecureRandom secureRandom = SecureRandom.getInstance("SHA1PRNG");
    
    SecureRandom secureRandom = SecureRandom.getInstance("SHA1PRNG", "SUN");

3、正确使用的示例

    SecureRandom secureRandom = new SecureRandom();
    // 生成种子，种子的意思是SecureRandom基于此种子生成的随机数，因此不设置种子会默认提供不重复的种子
    byte[] seed = SecureRandom.getSeed(16);
    // 置入种子
    secureRandom.setSeed(seed);
    // 生成
    secureRandom.nextInt(63)
    // 重置种子
    secureRandom.nextBytes(seed);
