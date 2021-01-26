import lombok.extern.slf4j.Slf4j;
import org.apache.commons.codec.binary.Base64;

import javax.crypto.Cipher;
import javax.crypto.spec.IvParameterSpec;
import javax.crypto.spec.SecretKeySpec;
import java.nio.charset.StandardCharsets;
import java.security.AlgorithmParameters;

/**
 * 快手小程序解密算法
 *
 * 快手用的是PKCS5, 微信用的是PKCS7, 其余加密方式是一样的.
 * 这段代码copy自WxJava的解密代码, 只改了Cipher的transformation, 并去掉了PKCS7Encoder
 *
 * @author houseyoung
 */
@Slf4j
public class KuaishouDecryptUtils {
    public static String decrypt(String sessionKey, String encryptedData, String ivStr) {
        try {
            AlgorithmParameters params = AlgorithmParameters.getInstance("AES");
            params.init(new IvParameterSpec(Base64.decodeBase64(ivStr)));
            Cipher cipher = Cipher.getInstance("AES/CBC/PKCS5Padding");
            cipher.init(2, new SecretKeySpec(Base64.decodeBase64(sessionKey), "AES"), params);
            return new String(cipher.doFinal(Base64.decodeBase64(encryptedData)), StandardCharsets.UTF_8);
        } catch (Exception e) {
            log.error("[KuaishouDecryptUtils] decrypt 解密异常, sessionKey: {}, encryptedData: {}, ivStr: {}", sessionKey, encryptedData, ivStr, e);
            return null;
        }
    }
}
