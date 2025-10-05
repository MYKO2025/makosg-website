# makosg-website
import React, { useState, useEffect } from "react";

// Load Josefin Sans font in your index.html or via CSS:
// <link href="https://fonts.googleapis.com/css2?family=Josefin+Sans:wght@400;600;700&display=swap" rel="stylesheet" />

const josefinFont = "'Josefin Sans', sans-serif";
const mainBgColor = "#a9bcdc";
const navGradient = "linear-gradient(to right, white, #738080)";

const socialIcons = {
  instagram: (
    <svg
      xmlns="http://www.w3.org/2000/svg"
      fill="#738080"
      viewBox="0 0 24 24"
      width="32px"
      height="32px"
      aria-hidden="true"
    >
      <path d="M7.75 2h8.5A5.75 5.75 0 0122 7.75v8.5A5.75 5.75 0 0116.25 22h-8.5A5.75 5.75 0 012 16.25v-8.5A5.75 5.75 0 017.75 2zm0 2A3.75 3.75 0 004 7.75v8.5A3.75 3.75 0 007.75 20h8.5a3.75 3.75 0 003.75-3.75v-8.5A3.75 3.75 0 0016.25 4h-8.5zm8.75 1.5a1 1 0 110 2 1 1 0 010-2zM12 7a5 5 0 110 10 5 5 0 010-10zm0 2a3 3 0 100 6 3 3 0 000-6z" />
    </svg>
  ),
  linkedin: (
    <svg
      xmlns="http://www.w3.org/2000/svg"
      fill="#738080"
      viewBox="0 0 24 24"
      width="32px"
      height="32px"
      aria-hidden="true"
    >
      <path d="M4.98 3.5C4.98 4.88 3.88 6 2.5 6S0 4.88 0 3.5 1.12 1 2.5 1 4.98 2.12 4.98 3.5zM0 8h5v16H0V8zm7.5 0h4.8v2.2h.1c.7-1.3 2.4-2.7 4.9-2.7 5.2 0 6.2 3.4 6.2 7.8V24h-5v-7.5c0-1.8 0-4-2.5-4s-2.9 2-2.9 3.9V24h-5V8z" />
    </svg>
  ),
  youtube: (
    <svg
      xmlns="http://www.w3.org/2000/svg"
      fill="#738080"
      viewBox="0 0 24 24"
      width="32px"
      height="32px"
      aria-hidden="true"
    >
      <path d="M23.5 6.2a2.8 2.8 0 00-1.97-2c-1.74-.47-8.73-.47-8.73-.47s-6.99 0-8.73.47a2.8 2.8 0 00-1.97 2A29.5 29.5 0 001 12a29.5 29.5 0 00.1 5.8 2.8 2.8 0 001.97 2c1.74.47 8.73.47 8.73.47s6.99 0 8.73-.47a2.8 2.8 0 001.97-2A29.5 29.5 0 0024 12a29.5 29.5 0 00-.5-5.8zM10 16V8l6 4-6 4z" />
    </svg>
  ),
};

type Page =
  | "HOME"
  | "MAKO"
  | "TEAM"
  | "SPONSORHIPS"
  | "CONTACT US"
  | "MAKO II"
  | "MAKO I"
  | "2026 TEAM"
  | "2025 TEAM"
  | "2024 TEAM"
  | "2026 SPONSORS"
  | "2025 SPONSORS"
  | "2024 SPONSORS"
  | "SUPPORT US";

const Title = ({
  children,
  size,
  weight,
  style,
}: {
  children: React.ReactNode;
  size: number;
  weight: "regular" | "semibold" | "bold";
  style?: React.CSSProperties;
}) => {
  let fontWeightNum = 400;
  if (weight === "semibold") fontWeightNum = 600;
  else if (weight === "bold") fontWeightNum = 700;
  return (
    <div
      style={{
        fontFamily: josefinFont,
        fontWeight: fontWeightNum,
        fontSize: size,
        lineHeight: 1.1,
        ...style,
      }}
    >
      {children}
    </div>
  );
};

const PlaceholderBox = ({
  width,
  height,
  style,
  onClick,
  children,
  alt,
}: {
  width: number | string;
  height: number | string;
  style?: React.CSSProperties;
  onClick?: () => void;
  children?: React.ReactNode;
  alt?: string;
}) => (
  <div
    onClick={onClick}
    role={onClick ? "button" : undefined}
    tabIndex={onClick ? 0 : undefined}
    onKeyDown={
      onClick
        ? (e) => {
            if (e.key === "Enter" || e.key === " ") {
              e.preventDefault();
              onClick();
            }
          }
        : undefined
    }
    style={{
      width,
      height,
      backgroundColor: "#d0d7e6",
      border: "2px dashed #738080",
      borderRadius: 8,
      display: "flex",
      justifyContent: "center",
      alignItems: "center",
      cursor: onClick ? "pointer" : "default",
      userSelect: "none",
      ...style,
    }}
    aria-label={alt || "Placeholder box"}
  >
    {children}
  </div>
);

const ImageSlider = () => {
  const images = [
    "https://via.placeholder.com/900x300?text=Slide+1",
    "https://via.placeholder.com/900x300?text=Slide+2",
    "https://via.placeholder.com/900x300?text=Slide+3",
  ];
  const [current, setCurrent] = useState(0);

  useEffect(() => {
    const interval = setInterval(() => {
      setCurrent((c) => (c + 1) % images.length);
    }, 4000);
    return () => clearInterval(interval);
  }, []);

  return (
    <div
      style={{
        width: "100%",
        maxWidth: 900,
        height: 300,
        margin: "0 auto",
        position: "relative",
        borderRadius: 8,
        overflow: "hidden",
        boxShadow: "0 4px 8px rgba(0,0,0,0.1)",
      }}
    >
      {images.map((src, i) => (
        <img
          key={i}
          src={src}
          alt={`Slide ${i + 1}`}
          style={{
            width: "100%",
            height: "100%",
            objectFit: "cover",
            position: "absolute",
            top: 0,
            left: 0,
            opacity: i === current ? 1 : 0,
            transition: "opacity 1s ease-in-out",
          }}
        />
      ))}
    </div>
  );
};

const SocialMediaRow = () => (
  <div
    style={{
      display: "flex",
      gap: 24,
      marginTop: 16,
      justifyContent: "center",
    }}
  >
    <a
      href="https://instagram.com"
      target="_blank"
      rel="noopener noreferrer"
      aria-label="Instagram"
      style={{ display: "inline-block" }}
    >
      {socialIcons.instagram}
    </a>
    <a
      href="https://linkedin.com"
      target="_blank"
      rel="noopener noreferrer"
      aria-label="LinkedIn"
      style={{ display: "inline-block" }}
    >
      {socialIcons.linkedin}
    </a>
    <a
      href="https://youtube.com"
      target="_blank"
      rel="noopener noreferrer"
      aria-label="YouTube"
      style={{ display: "inline-block" }}
    >
      {socialIcons.youtube}
    </a>
  </div>
);

const NavBar = ({
  currentPage,
  onNavigate,
}: {
  currentPage: Page;
  onNavigate: (page: Page) => void;
}) => (
  <nav
    style={{
      background: navGradient,
      padding: "1rem 2rem",
      display: "flex",
      justifyContent: "center",
      gap: "3rem",
      fontFamily: josefinFont,
      fontWeight: 700,
      fontSize: 18,
      userSelect: "none",
      position: "sticky",
      top: 0,
      zIndex: 1000,
    }}
  >
    {["HOME", "MAKO", "TEAM", "SPONSORHIPS", "CONTACT US"].map((title) => (
      <button
        key={title}
        onClick={() => onNavigate(title as Page)}
        style={{
          background: "none",
          border: "none",
          cursor: "pointer",
          color: currentPage === title ? "#738080" : "#000",
          fontWeight: currentPage === title ? 800 : 700,
          fontSize: 18,
          padding: "0.25rem 0.5rem",
          letterSpacing: 1.2,
        }}
        aria-current={currentPage === title ? "page" : undefined}
      >
        {title}
      </button>
    ))}
  </nav>
);

const Home = ({ onNavigate }: { onNavigate: (page: Page) => void }) => (
  <main
    style={{
      backgroundColor: mainBgColor,
      minHeight: "100vh",
      padding: "1rem 2rem 4rem",
      color: "#000",
      fontFamily: josefinFont,
    }}
  >
    <div style={{ marginTop: 16 }}>
      <ImageSlider />
    </div>

    <div
      style={{
        display: "flex",
        justifyContent: "center",
        gap: 32,
        marginTop: 48,
        flexWrap: "wrap",
        alignItems: "center",
        maxWidth: 1200,
        marginLeft: "auto",
        marginRight: "auto",
      }}
    >
      <div style={{ flex: "1 1 400px", minWidth: 300 }}>
        <Title size={48} weight="bold" style={{ marginBottom: 16 }}>
          What is Mako
        </Title>
        <Title size={40} weight="regular" style={{ maxWidth: 600 }}>
          MAKO was previously known as Nautical Knights, started in 2024 by the very
          first captain Dong…
        </Title>
      </div>
      <PlaceholderBox
        width={300}
        height={300}
        alt="Photo of the captain"
        style={{ flexShrink: 0 }}
      >
        <span style={{ color: "#738080" }}>Captain Photo</span>
      </PlaceholderBox>
    </div>

    <div
      style={{
        marginTop: 96,
        maxWidth: 1200,
        marginLeft: "auto",
        marginRight: "auto",
        textAlign: "center",
      }}
    >
      <Title size={48} weight="bold" style={{ marginBottom: 8 }}>
        CONTACT US
      </Title>
      <div style={{ fontSize: 24, marginBottom: 48 }}>
        teammakosg@gmail.com
      </div>

      <Title size={48} weight="bold" style={{ marginBottom: 8 }}>
        FOLLOW US ON SOCIAL MEDIA
      </Title>
      <SocialMediaRow />
    </div>
  </main>
);

const Mako = ({ onNavigate }: { onNavigate: (page: Page) => void }) => (
  <main
    style={{
      backgroundColor: mainBgColor,
      minHeight: "100vh",
      padding: "2rem",
      fontFamily: josefinFont,
      color: "#000",
      maxWidth: 1200,
      margin: "0 auto",
    }}
  >
    <div style={{ marginBottom: 48 }}>
      <div style={{ marginBottom: 16 }}>
        <Title size={96} weight="bold" style={{ marginBottom: 8 }}>
          MAKO II
        </Title>
        <Title size={40} weight="regular" style={{ marginBottom: 16 }}>
          competed in ISR 2025
        </Title>
        <PlaceholderBox
          width="100%"
          height={300}
          alt="MAKO II photo"
          onClick={() => onNavigate("MAKO II")}
          style={{ cursor: "pointer" }}
        >
          <span style={{ color: "#738080" }}>Click to view MAKO II photos</span>
        </PlaceholderBox>
      </div>

      <div>
        <Title size={96} weight="bold" style={{ marginBottom: 8 }}>
          MAKO I
        </Title>
        <Title size={40} weight="regular" style={{ marginBottom: 16 }}>
          competed in EISR 2024
        </Title>
        <PlaceholderBox
          width="100%"
          height={300}
          alt="MAKO I photo"
          onClick={() => onNavigate("MAKO I")}
          style={{ cursor: "pointer" }}
        >
          <span style={{ color: "#738080" }}>Click to view MAKO I photos</span>
        </PlaceholderBox>
      </div>
    </div>
  </main>
);

const MakoDetail = ({
  title,
  onNavigate,
}: {
  title: "MAKO I" | "MAKO II";
  onNavigate: (page: Page) => void;
}) => (
  <main
    style={{
      backgroundColor: mainBgColor,
      minHeight: "100vh",
      padding: "2rem",
      fontFamily: josefinFont,
      color: "#000",
      maxWidth: 1200,
      margin: "0 auto",
    }}
  >
    <Title size={96} weight="semibold" style={{ marginBottom: 32 }}>
      {title}
    </Title>
    <div
      style={{
        display: "grid",
        gridTemplateColumns: "repeat(auto-fit,minmax(150px,1fr))",
        gap: 16,
      }}
    >
      {Array.from({ length: 10 }).map((_, i) => (
        <PlaceholderBox
          key={i}
          width="100%"
          height={150}
          alt={`${title} photo ${i + 1}`}
        >
          <span style={{ color: "#738080" }}>{`Photo ${i + 1}`}</span>
        </PlaceholderBox>
      ))}
    </div>
  </main>
);

const Team = ({ onNavigate }: { onNavigate: (page: Page) => void }) => {
  const teams = [
    { year: "2026", photos: 32 },
    { year: "2025", photos: 22 },
    { year: "2024", photos: 15 },
  ];
  return (
    <main
      style={{
        backgroundColor: mainBgColor,
        minHeight: "100vh",
        padding: "2rem",
        fontFamily: josefinFont,
        color: "#000",
        maxWidth: 1200,
        margin: "0 auto",
      }}
    >
      {teams.map(({ year }) => (
        <div key={year} style={{ marginBottom: 48 }}>
          <button
            onClick={() => onNavigate(`${year} TEAM` as Page)}
            style={{
              background: "none",
              border: "none",
              cursor: "pointer",
              fontFamily: josefinFont,
              fontWeight: 700,
              fontSize: 64,
              color: "#000",
              marginBottom: 16,
              textDecoration: "underline",
              padding: 0,
            }}
            aria-label={`Go to ${year} Team page`}
          >
            {year} Team
          </button>
          <PlaceholderBox
            width="100%"
            height={200}
            alt={`${year} Team photo`}
          >
            <span style={{ color: "#738080" }}>{`${year} Team Photo`}</span>
          </PlaceholderBox>
        </div>
      ))}
    </main>
  );
};

const TeamDetail = ({
  year,
  count,
}: {
  year: string;
  count: number;
}) => (
  <main
    style={{
      backgroundColor: mainBgColor,
      minHeight: "100vh",
      padding: "2rem",
      fontFamily: josefinFont,
      color: "#000",
      maxWidth: 1200,
      margin: "0 auto",
    }}
  >
    <Title size={96} weight="bold" style={{ marginBottom: 32 }}>
      {year} TEAM
    </Title>
    <div
      style={{
        display: "grid",
        gridTemplateColumns: "repeat(auto-fit,minmax(120px,1fr))",
        gap: 16,
      }}
    >
      {Array.from({ length: count }).map((_, i) => (
        <PlaceholderBox
          key={i}
          width="100%"
          height={120}
          alt={`${year} team photo ${i + 1}`}
        >
          <span style={{ color: "#738080" }}>{`Photo ${i + 1}`}</span>
        </PlaceholderBox>
      ))}
    </div>
  </main>
);

const Sponsorships = ({ onNavigate }: { onNavigate: (page: Page) => void }) => (
 

